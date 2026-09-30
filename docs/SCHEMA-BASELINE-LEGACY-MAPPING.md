# PDISC-1B — Legacy Kalam Connect Schema Baseline & Target Mapping

**Date:** 30/09/2026  
**Status:** WORKING BASELINE — schema/data migration planning, no DDL applied

## Decision

Use the existing Kalam Connect data as the migration baseline, but do **not** reproduce the Webflow CMS structure literally.

Migration sources:

1. **People / Kalam App** → shared Kalam People Database.
2. **Categories - Connects** → seed the initial Connect category taxonomy.
3. **Kalam Connects** → migrate into native Connect publications and related records.

The goal is **lossless migration with a better application schema**.

---

# 1. People — reference, do not duplicate

## Existing Webflow source

Legacy Webflow collection:

`Teams`

Observed fields include:

- Employeer ID
- Photo
- Hover Photo
- Job Title
- Email
- Hiring Date
- Date of Birth
- Country
- Region
- Department
- Number of Awards
- Phraise Form
- Photo Gallery
- Not Active?
- is a Manager?
- Order
- Name
- Slug

Observed item count during audit: **1,275**.

## Existing shared Supabase authority

Project:

`Kalam People Database`

Current relevant tables:

### `kalam_people`
- **2,309 rows**
- normalized Kalam App mirror;
- Kalam App remains source of truth;
- primary identity = `kalam_app_id`;
- includes first/last/full name, business email, DOB, hiring date, status, module/account/language, title, country/nationality and source traceability.

### `people`
- canonical reconciled human identity;
- UUID primary key;
- currently contains only verified/reconciled identities, so it must not be assumed to cover every Kalam App person yet.

### `person_source_refs`
- maps source identities such as Kalam App and Webflow item IDs to canonical people;
- allows unresolved records without guessing identity.

### `person_media`
- verified current profile media and source lineage;
- copied to controlled Supabase Storage.

## Target Connect rule

**Do not create another employee master table inside Kalam Connect.**

Connect owns only the member/social layer.

Target conceptual table:

### `profiles`

- `id uuid`
- `auth_user_id uuid unique`
- `kalam_app_id text unique not null`
- `person_id uuid nullable` — canonical People UUID when verified
- `username/handle`
- `bio`
- `cover_media_id`
- `profile_preferences`
- `account_state`
- `created_at`
- `updated_at`

Company-controlled display data is resolved from the People projection.

Do not duplicate private People fields such as:
- personal email;
- phone/WhatsApp;
- raw source JSON;
- HR-only attributes.

## Transitional identity rule

Because the canonical `people` table is not yet fully reconciled for the entire Kalam App population:

- use `kalam_app_id` as the stable required source identity for initial Connect provisioning;
- add `person_id` when canonical reconciliation exists;
- never guess a canonical person from name alone;
- email is an authentication/lookup attribute, not the permanent person primary key.

---

# 2. Categories — migrate as seed taxonomy

## Existing Webflow collection

`Categories - Connects`

Fields:

- Name
- Slug
- Cover
- Connect Hero
- Summary
- Color

Current 12 categories:

1. Announcements
2. Birthday
3. Celebration
4. Community
5. Events
6. Leader of the month
7. Promotions
8. Recognition
9. Tips
10. Top Performers
11. Training & Development
12. Vacancies

## Target table

### `categories`

Recommended fields:

- `id uuid`
- `legacy_webflow_id text unique nullable`
- `name text`
- `slug text unique`
- `summary text nullable`
- `cover_media_id uuid nullable`
- `hero_media_id uuid nullable`
- `accent_token text nullable`
- `legacy_color text nullable`
- `active boolean`
- `sort_order integer nullable`
- `created_at`
- `updated_at`

## Important improvement — Category ≠ Publication Type

The legacy system uses categories for both:
- editorial taxonomy;
- content behavior.

The new product should separate them.

Example:

```text
publication_type = recognition
category = Recognition

publication_type = recognition
category = Top Performers

publication_type = event
category = Events

publication_type = article
category = Training & Development
```

This keeps UI/business behavior stable even if Marketing later renames or reorganizes categories.

The 12 legacy categories should still be imported unchanged as the initial taxonomy.

---

# 3. Legacy Connect Posts

## Existing Webflow collection

`Kalam Connects`

Observed generic fields:

- Name
- Slug
- Publish Date
- Thumbnail
- Email Marketing
- Primary Category
- Summary
- Card Link Text
- Featured
- Pinned
- Article
- Team Members

Media/content-mode fields:

- Single Video
- Video
- Video Gallery
- Image Gallery
- Image Gallery 02
- Form
- Form Link

Vacancy-specific fields:

- About Vacancy
- About Vacancy Image
- Requirements
- Duties & Responsibilities
- Closing Date
- Apply for Vacancy Email

The existing collection therefore mixes multiple content types in one flat CMS item.

Recent live items confirm the collection currently carries:
- birthdays;
- anniversaries;
- Top Performers;
- people-linked celebrations;
- other official Connect content.

One Top Performers item already references many Team Members, proving the target schema must natively support **one publication → many people**.

---

# 4. Target publication schema

## `publications`

Core canonical official content object.

Recommended baseline:

- `id uuid`
- `legacy_webflow_id text unique nullable`
- `legacy_slug text nullable`
- `slug text unique`
- `title text`
- `summary text nullable`
- `body rich/json/text nullable`
- `publication_type text`
- `primary_category_id uuid nullable`
- `status text`
- `publish_at timestamptz nullable`
- `expire_at timestamptz nullable`
- `archive_at timestamptz nullable`
- `featured boolean`
- `pinned boolean`
- `reactions_enabled boolean`
- `sharing_enabled boolean`
- `source text` — migrated/manual/automation/etc.
- `source_ref text nullable`
- `campaign_ref text nullable`
- `created_by_profile_id uuid nullable`
- `published_by_profile_id uuid nullable`
- `type_data jsonb default '{}'`
- `legacy_data jsonb default '{}'`
- `created_at`
- `updated_at`

### Why keep `legacy_data`

Migration must be lossless.

Any old field that does not yet have a native destination remains preserved in `legacy_data` during migration.

It is not the long-term application API.

---

# 5. Publication ↔ People

## `publication_people`

Many-to-many relationship.

Recommended:

- `publication_id`
- `kalam_app_id`
- `person_id nullable`
- `profile_id nullable`
- `relationship_type`
- `sort_order`
- `metadata`

Initial relationship types:

- subject
- tagged
- recognized
- top_performer
- birthday_person
- anniversary_person
- promoted_person
- featured_person
- author
- mentioned

This replaces the Webflow `Team Members` multi-reference with explicit semantics.

---

# 6. Publication ↔ Categories

Keep a primary category for easy editorial behavior.

Recommended:

### `publication_categories`

- `publication_id`
- `category_id`
- `is_primary boolean`
- `sort_order`

Even if the legacy source has only one Primary Category, the native model should allow additional categories/topics later without schema redesign.

---

# 7. Media normalization

Do not recreate these as separate columns:

- Thumbnail
- Email Marketing
- About Vacancy Image
- Gallery
- Image Gallery 02
- Video
- Video Gallery

Use:

### `media_assets`

Reusable stored asset metadata.

### `publication_media`

- `publication_id`
- `media_asset_id`
- `role`
- `sort_order`
- `metadata`

Initial roles:

- thumbnail
- cover
- main
- email
- hero
- gallery
- gallery_secondary
- video
- vacancy
- attachment

This makes the same approved image reusable across Magazine, Timeline, email, profile projections and future channel adapters.

---

# 8. Type-specific data

The old CMS has vacancy-only fields mixed into every post.

For PDISC-1B baseline, preserve structured type data in:

`publications.type_data jsonb`

Example vacancy:

```json
{
  "about": "...",
  "requirements": "...",
  "duties_responsibilities": "...",
  "closing_date": "...",
  "apply_email": "...",
  "form_url": "..."
}
```

If a publication type later needs heavy querying, constraints or independent lifecycle, promote that structure into a dedicated typed table.

This avoids creating many empty columns while keeping MVP migration simple.

---

# 9. Forms

Legacy:
- `Form` switch
- `Form Link`

Target:

Do not make a boolean `form` property part of every publication forever.

Use a CTA/action model:

### `publication_actions`

- `publication_id`
- `action_type`
- `label`
- `url`
- `metadata`
- `sort_order`

Examples:
- apply
- register
- survey
- external_link
- internal_route
- download

The old Form Link becomes an action during migration.

---

# 10. Legacy field mapping

| Webflow Kalam Connect field | Native target |
|---|---|
| Name | publications.title |
| Slug | publications.slug + legacy_slug |
| Publish Date | publications.publish_at |
| Thumbnail | publication_media role=thumbnail |
| Email Marketing | publication_media role=email |
| Primary Category | publication_categories is_primary=true |
| Summary | publications.summary |
| Card Link Text | publication_actions label or legacy_data |
| Featured | publications.featured |
| Pinned | publications.pinned |
| Article | publications.body |
| Team Members | publication_people |
| Single Video | type/media presentation metadata |
| Video | publication_media role=video |
| Video Gallery | publication_media/video references |
| Image Gallery | publication_media role=gallery |
| Image Gallery 02 | publication_media role=gallery_secondary |
| Form | publication_actions / migrated metadata |
| Form Link | publication_actions |
| About Vacancy | type_data.about |
| About Vacancy Image | publication_media role=vacancy |
| Requirements | type_data.requirements |
| Duties & Responsibilities | type_data.duties_responsibilities |
| Closing Date | type_data.closing_date |
| Apply for Vacancy Email | type_data.apply_email |

---

# 11. Recommended database boundary

## Preferred

**Keep Kalam Connect as a separate application database/project.**

Consume a minimal, approved People projection keyed by `kalam_app_id`.

Reasons:

- Connect is its own product authority;
- separate RLS/auth/social tables reduce blast radius;
- private messages/community data remain isolated from Marketing automation tables;
- the current Kalam People project already contains People plus Marketing/AI orchestration state;
- a Connect mistake should not endanger the shared People/automation project;
- Connect can deploy/migrate independently.

## Do not

Do not place the entire social network directly into the current Kalam People Database merely because employee data is already there.

That project currently also contains:
- content request state;
- content draft state;
- AI identities/connectors;
- approvals/activity logs;
- release jobs;
- evidence packages/assets;
- creative assets.

Kalam Connect needs an explicit boundary.

## People projection options

Final technical choice belongs to KC1/KC2, but acceptable patterns include:

1. controlled sync of eligible People fields into a Connect member directory;
2. trusted server lookup plus cached projection;
3. event-driven People → Connect synchronization.

Do not duplicate the full raw Kalam App record.

---

# 12. PDISC-1B baseline outcome

Use the current production data model as the migration source:

```text
Kalam App / People
        ↓
Connect profile link

Legacy Categories
        ↓
categories

Legacy Kalam Connects
        ↓
publications
├── publication_people
├── publication_categories
├── publication_media
├── publication_actions
└── type_data
```

This preserves all existing Kalam Connect content while giving the new product clean foundations for:

- Magazine;
- Timeline shares;
- tagged-profile projections;
- reactions;
- comments;
- automation;
- future search/filtering;
- future content types.

No production schema or data has been changed by this document.
