# PDISC-1B — Publication Types & Field Matrix

**Decision date:** 30/09/2026  
**Status:** LOCKED  
**Scope:** Official Kalam Connect publications and legacy Webflow migration

## Core decision

Do not make every legacy category a hard-coded application type.

Use three separate concepts:

```text
Publication Type
= application behavior

Publication Subtype
= specific behavior variant

Category
= editorial taxonomy / filtering / visual grouping
```

Example:

```text
type = recognition
subtype = top_performers
category = Top Performers
```

or:

```text
type = people_milestone
subtype = birthday
category = Birthday
```

This preserves all existing Kalam Connect categories while preventing category names from controlling database/application behavior.

---

# 1. Locked publication types

Initial native types:

1. `story`
2. `announcement`
3. `recognition`
4. `people_milestone`
5. `event`
6. `opportunity`
7. `poll`
8. `community_feature`

Do not implement these as a PostgreSQL ENUM unless KC3 decides there is a strong reason.

Preferred:
- text/slug;
- foreign key to a controlled `publication_types` registry.

This allows controlled extension without destructive schema migrations.

---

# 2. Legacy category mapping

| Legacy category | Native type | Default subtype | People rule | Period/date rule |
|---|---|---|---|---|
| Announcements | announcement | general | optional | optional |
| Birthday | people_milestone | birthday | required | optional |
| Celebration | people_milestone | celebration | optional | optional |
| Community | community_feature | general | optional | optional |
| Events | event | general | optional | event date/time when applicable |
| Leader of the month | recognition | leader_of_month | required | required |
| Promotions | people_milestone | promotion | required | optional |
| Recognition | recognition | general | required | optional |
| Tips | story | tips | optional | optional |
| Top Performers | recognition | top_performers | required, multi-person supported | required |
| Training & Development | story | training | optional | optional |
| Vacancies | opportunity | vacancy | optional | closing date optional/required by business policy |

These mappings preserve the existing Webflow categories and current Automation `content_request_categories` semantics.

---

# 3. Additional native subtypes

The product already requires cases that are not first-class legacy categories.

Initial subtype registry should also allow:

### people_milestone
- birthday
- anniversary
- promotion
- welcome
- celebration

### recognition
- general
- top_performers
- leader_of_month
- award

### story
- general
- tips
- training
- feature

### announcement
- general
- urgent
- policy
- operational

### event
- general
- social
- training
- company
- external

### opportunity
- vacancy
- internal_opportunity
- survey
- application

### poll
- opinion
- survey

### community_feature
- general
- community_highlight
- initiative

Subtype values are controlled configuration, not free-form member input.

---

# 4. Universal publication fields

Every official publication has:

| Field | Required | Notes |
|---|---:|---|
| id | yes | UUID |
| title | yes | Member-facing title |
| slug | yes | Unique URL identifier |
| publication_type | yes | FK/type registry |
| publication_subtype | optional | Controlled subtype |
| status | yes | draft/review/scheduled/published/archived/withdrawn |
| source | yes | migrated/manual/automation/system |
| summary | optional | Card/detail summary |
| body | optional | Rich publication body |
| primary_category_id | optional | Primary editorial category |
| publish_at | conditional | Required to publish immediately/schedule |
| expire_at | optional | Publication visibility expiry |
| archive_at | optional | Archive transition |
| featured | yes/default false | Publication-level editorial flag |
| pinned | yes/default false | Publication-level editorial flag |
| reactions_enabled | yes/default true | Staff/type default override |
| sharing_enabled | yes/default true | Staff/type default override |
| campaign_ref | optional | Cross-channel campaign reference |
| source_ref | optional | Legacy/automation/source reference |
| created_by_profile_id | conditional | Required for manual staff creation |
| published_by_profile_id | conditional | Human/service release authority |
| type_data | yes/default {} | Controlled type-specific structured data |
| legacy_data | yes/default {} | Migration preservation only |
| created_at | yes | System |
| updated_at | yes | System |

Other relationships are normalized:
- people;
- categories;
- media;
- actions;
- placements;
- audiences.

---

# 5. Type matrix

## A. Story

Purpose:
- general editorial article;
- Tips;
- Training & Development;
- feature stories.

Required:
- title;
- type;
- body OR meaningful media/summary;
- at least one publication surface/placement for release.

Optional:
- summary;
- people;
- categories;
- gallery/video;
- CTA/actions.

Default:
- reactions enabled;
- sharing enabled.

Recommended card variants:
- Hero
- Feature
- Standard
- Compact

Automation:
- may create/update draft;
- may populate title/summary/body/media/category;
- human controls final editorial placement unless an approved release contract explicitly permits otherwise.

---

## B. Announcement

Purpose:
- official information members need to know.

Required:
- title;
- meaningful body OR summary.

Optional:
- effective date;
- expiry;
- people;
- CTA;
- attachment;
- urgency level.

`type_data` keys:
- `urgency`
- `effective_at`
- `acknowledgement_required` — reserved, default false

Default:
- reactions configurable;
- sharing enabled unless staff disables.

Recommended cards:
- Announcement
- Feature
- Compact

Automation:
- may draft;
- urgent/operational auto-release requires a later explicit policy and is not assumed.

---

## C. Recognition

Purpose:
- recognize one or many people.

Required:
- at least one related person;
- relationship type;
- title;
- recognition context/summary.

Optional:
- body;
- period label;
- achievement details;
- media.

`type_data` keys:
- `period_label`
- `achievement_summary`
- `recognition_label`

People relationship rules:

### general recognition
- `recognized`

### Top Performers
- `top_performer`
- one or many people;
- period required.

### Leader of the Month
- `leader_of_month`
- one or many people allowed by current automation;
- period required.

Default:
- reactions enabled;
- sharing enabled;
- automatic tagged/profile/recognition projection enabled.

Recommended cards:
- Person / Recognition
- Feature
- Hero where manually selected

Automation:
- may resolve people by stable Kalam identity;
- may generate draft copy/creative;
- cannot invent achievements/performance claims;
- final people selection must match approved source evidence.

---

## D. People Milestone

Purpose:
- personal/company milestones involving Kalam members.

Subtypes:
- birthday;
- anniversary;
- promotion;
- welcome;
- celebration.

### Birthday
Required:
- one or many people.
Date source:
- People record / approved campaign date.

### Anniversary
Required:
- one or many people.
Derived/explicit:
- anniversary year/period may be computed from hiring date but should be recorded in release package.

### Promotion
Required:
- one or many people;
- new role/context when available.

### Welcome
Required:
- one or many people.

### Celebration
People optional because some celebrations are company-wide.

`type_data` keys may include:
- `milestone_date`
- `years`
- `new_title`
- `occasion_label`

Default:
- reactions enabled;
- sharing enabled;
- tagged/profile projection enabled when people exist.

Recommended cards:
- Person / Recognition
- Feature
- Standard

Automation:
- may derive birthday/anniversary candidate from People source;
- may create draft;
- must not fabricate personal facts.

---

## E. Event

Purpose:
- event information and registration/discovery.

Required when applicable:
- title;
- event start date/time OR explicit event date label.

Optional:
- end time;
- location;
- online URL;
- host/organizer;
- related people;
- capacity;
- registration action;
- cover/gallery.

`type_data`:
- `starts_at`
- `ends_at`
- `location`
- `location_url`
- `host_label`
- `capacity`
- `registration_deadline`

Actions:
- register;
- calendar;
- external link.

Default:
- reactions enabled;
- sharing enabled.

Recommended cards:
- Event
- Hero
- Feature
- Standard

---

## F. Opportunity

Purpose:
- internal vacancy or other actionable opportunity.

Subtype `vacancy` preserves current Webflow vacancy behavior.

Required for vacancy:
- title;
- opportunity/vacancy body or about text.

Optional:
- requirements;
- duties/responsibilities;
- closing date;
- apply email;
- application URL;
- related people;
- department/team;
- vacancy media.

`type_data`:
- `about`
- `requirements`
- `duties_responsibilities`
- `closing_date`
- `apply_email`
- `department`
- `location`

Actions:
- apply;
- external_link;
- internal_route.

Default:
- reactions configurable;
- sharing enabled.

Recommended cards:
- Opportunity
- Feature
- Standard

Legacy mappings:
- About Vacancy → type_data.about
- Requirements → type_data.requirements
- Duties & Responsibilities → type_data.duties_responsibilities
- Closing Date → type_data.closing_date
- Apply Email → type_data.apply_email
- Form Link → action

---

## G. Poll

Purpose:
- lightweight member opinion or structured prompt.

Required:
- title/question;
- at least two choices.

`type_data`:
- `question`
- `choices`
- `multiple_choice`
- `closes_at`
- `results_visibility`

Important:
poll responses require their own normalized response/vote table during implementation.

Do not store all votes inside publication JSON.

Default:
- sharing configurable;
- reactions configurable.

Recommended card:
- Poll

---

## H. Community Feature

Purpose:
- editorially highlight a Community, initiative, group activity, or member-created community story.

Required:
- title;
- community reference OR meaningful editorial body.

Optional:
- people;
- gallery;
- community CTA.

`type_data`:
- `feature_kind`
- `community_ref`

Default:
- reactions enabled;
- sharing enabled.

Recommended cards:
- Feature
- Standard
- Community-specific card in later design phase.

---

# 6. People relationship matrix

| Type | People requirement | Multiple | Automatic profile projection |
|---|---|---:|---|
| story | optional | yes | only explicit tagged/featured people |
| announcement | optional | yes | only explicit tagged people |
| recognition | required | yes | yes |
| people_milestone | subtype-dependent; generally required | yes | yes when people exist |
| event | optional | yes | only explicit tagged/hosted people |
| opportunity | optional | yes | only explicit tagged people |
| poll | optional | yes | only explicit tagged people |
| community_feature | optional | yes | only explicit tagged/featured people |

Relationship type, not just presence in `publication_people`, determines projection behavior.

---

# 7. Media slots

Normalize through `publication_media`.

Supported initial roles:

- thumbnail;
- cover;
- hero;
- main;
- email;
- gallery;
- gallery_secondary;
- video;
- vacancy;
- attachment.

Rules:
- one media asset may be reused in multiple roles/publications;
- order is explicit;
- role compatibility may be validated by publication type;
- legacy Webflow URLs/assets are preserved in migration provenance;
- verified employee faces remain sourced from approved person media.

---

# 8. Actions

Normalize through `publication_actions`.

Initial action types:
- read_more;
- apply;
- register;
- survey;
- external_link;
- internal_route;
- download;
- calendar.

Each action:
- publication;
- type;
- label;
- URL/route;
- sort order;
- metadata.

Do not keep legacy `Form=true` as a permanent universal field.

---

# 9. Placement compatibility

All official types can appear in Magazine if staff chooses.

Default preferred placements:

| Type | Magazine | Official Timeline | Profile projection | Community | Specialized surface |
|---|---:|---:|---:|---:|---|
| story | yes | optional | tagged only | optional | no |
| announcement | yes | optional | tagged only | optional | Announcements |
| recognition | yes | yes | yes | optional | Recognitions |
| people_milestone | yes | yes | yes | optional | People/Recognitions |
| event | yes | optional | tagged only | optional | Events |
| opportunity | yes | optional | tagged only | optional | Opportunities |
| poll | yes | optional | tagged only | optional | Polls if later added |
| community_feature | yes | optional | tagged only | yes | Communities |

"Official Timeline" means a deliberate official projection. Magazine publication does not automatically become a Timeline post unless placement rules say so.

Tagged-person relevance/projection remains independent of official Timeline placement.

---

# 10. Manual vs automation ownership

## Staff may
- create any official publication type;
- edit all normal publication fields;
- select/resolve people;
- choose categories;
- upload/select media;
- add actions;
- choose audience;
- choose placement;
- review;
- approve;
- schedule;
- publish;
- archive.

## Automation may
- create/update drafts;
- populate source-backed fields;
- resolve people using stable identities;
- attach campaign/source references;
- attach approved assets;
- populate type_data supported by its contract;
- propose/supply category and subtype;
- propose placement metadata where permitted.

## Automation may not
- fabricate missing person facts;
- invent vacancy requirements/deadlines;
- invent recognition achievements;
- change Magazine layout hierarchy;
- bypass approval/release authority;
- silently change a human-edited field after review without creating a new revision/conflict state.

---

# 11. Type registry

Recommended future table:

### `publication_types`

Fields:
- `slug`
- `name`
- `active`
- `people_requirement`
- `allow_multiple_people`
- `period_requirement`
- `default_card_variant`
- `default_reactions_enabled`
- `default_sharing_enabled`
- `default_profile_projection`
- `config jsonb`

This is application configuration.

Do not reuse Automation's `content_request_categories` as the Connect application type registry; Automation categories remain upstream workflow configuration.

---

# 12. Migration rules

For every legacy Kalam Connect item:

1. preserve Webflow item ID;
2. preserve original slug;
3. resolve legacy category;
4. map category → default type/subtype;
5. copy title/date/summary/body;
6. migrate all media by role;
7. resolve Team Members through `person_source_refs` / stable Kalam identity where possible;
8. preserve unresolved member references rather than guessing;
9. convert form/form-link to actions;
10. convert vacancy fields to opportunity type_data;
11. preserve any unmapped field in `legacy_data`;
12. mark `source = migrated_webflow`;
13. preserve original publish status/timestamps where technically possible.

Migration must be idempotent.

---

# 13. PDISC-1B exit result

Locked:

- Category ≠ Publication Type.
- Behavior Type + Subtype model.
- Eight initial native publication types.
- Legacy 12-category mapping.
- Universal publication fields.
- Type-specific required/optional fields.
- People relationship rules.
- Media role model.
- Action model.
- Placement compatibility.
- Staff vs Automation ownership.
- Lossless migration rules.
- Configurable publication type registry rather than category-controlled behavior.

Next:
**PDISC-1C — Magazine Analytics, Moderation & Edge Cases.**
