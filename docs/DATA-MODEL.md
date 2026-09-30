# Kalam Connect — Data Model Plan

This document defines logical entities. Physical table names may change during implementation, but relationships and ownership should remain.

## Identity

### people_ref
Reference/projection to the shared Kalam People layer.

Minimum Connect-visible fields:
- stable_person_id;
- source;
- active/eligible state;
- approved name fields;
- department/team where appropriate;
- title/role where appropriate;
- verified image reference where available;
- source_updated_at.

Do not duplicate the entire employee database.

### profiles
Connect social identity.

Fields conceptually:
- id;
- auth_user_id;
- stable_person_id;
- username;
- display_name where policy allows;
- avatar;
- cover;
- bio;
- interests;
- profile_visibility;
- created_at;
- updated_at.

## Authorization

### roles
Global Connect roles.

### user_roles
Global role assignments.

### capabilities
Optional normalized capability catalog.

### community_roles / community_members
Scoped membership/admin/moderation authority.

## Magazine and social content

Use one common content foundation rather than one table per content type.

### publications
Official/staff/automation-backed Connect content.

Important fields:
- id;
- type;
- title;
- summary;
- body;
- status;
- author/profile or publisher reference;
- campaign_ref;
- content_package_ref;
- category_id;
- featured;
- pinned;
- audience_type;
- scheduled_at;
- published_at;
- expires_at;
- created_by;
- updated_by;
- automation_correlation_id;
- idempotency_key.

Lifecycle:
`draft → review → scheduled → published → archived`, with exceptional `withdrawn` state from scheduled/published content.

### publication_revisions
Immutable snapshots of official publication changes after review/publication.

Supports:
- revision number;
- snapshot;
- change summary;
- actor/source;
- approval reference;
- published revision tracking.

### magazine_analytics_events
Product engagement events for Magazine discovery/interaction.

Keep product analytics separate from privileged application audit.

Do not store publication bodies or private message contents in analytics events.

### member_posts
Member-authored timeline content.

Can later converge technically with publications if implementation proves one model is cleaner, but permissions/lifecycle must remain distinct.

### publication_people
Many-to-many relation between official content and people.

Supports:
- recognition;
- Top Performers;
- birthdays;
- anniversaries;
- welcome posts.

One publication may reference multiple people.

### categories
Magazine/topic categories.

### media
Normalized metadata around stored media where needed.

### comments
Threaded discussion on member posts and Timeline Shares. Canonical Magazine publications do not have one global comment thread; discussion occurs on the member's Timeline Share.

### reactions
Reaction target + actor + reaction type.

### bookmarks
Saved content.

### mentions
Optional normalized mention records for notifications/search.

## Communities

### communities
- id;
- name;
- slug;
- description;
- privacy;
- cover;
- rules;
- created_by;
- status.

### community_members
- community_id;
- profile_id;
- state;
- scoped_role;
- joined_at.

### community_posts
May be implemented as member_posts with community_id rather than a separate table.

Prefer the simplest model that preserves RLS clarity.

## Messaging

### conversations
- id;
- type: direct/group;
- title where group;
- created_by;
- created_at.

### conversation_participants
- conversation_id;
- profile_id;
- role;
- joined_at;
- left_at;
- last_read_at.

### messages
- id;
- conversation_id;
- sender_profile_id;
- body;
- reply_to_id;
- attachment refs;
- created_at;
- edited_at;
- deleted_at.

Private messages are not magazine/feed content.

## Notifications

### notifications
Created by trusted functions/triggers/server actions.

- recipient_profile_id;
- actor_profile_id where applicable;
- type;
- object_type;
- object_id;
- read_at;
- created_at;
- metadata.

Ordinary clients must not be able to forge arbitrary notifications.

### notification_preferences
Per member/event type.

## Moderation

### reports
- reporter;
- object type/id;
- reason;
- state;
- assigned moderator;
- resolution;
- timestamps.

### blocks
Member-to-member block relationships.

### mutes
Optional mute relationships.

### moderation_actions
Append-only moderator action evidence.

## Events and opportunities

### events
Internal member-facing event state.

### event_registrations

### vacancies
Internal opportunities/vacancies where Connect owns the presentation.

If another system is authoritative, store source references and projection state rather than duplicating business truth.

## Campaign/integration references

Cross-channel campaign orchestration is upstream.

Connect stores references, not a competing master campaign object.

### integration_receipts
Recommended for:
- correlation_id;
- capability;
- source_system;
- external_ref;
- object_ref;
- status;
- request version/hash;
- executed_at;
- error code.

This supports idempotency/reconciliation without exposing n8n internals to normal members.

## Audit

### staff_activity_log
Append-only high-value staff actions.

Include:
- actor;
- action;
- object;
- before/after reference or safe diff;
- correlation_id;
- outcome;
- timestamp.

## Retention principle

When a person's membership becomes inactive:
- disable/restrict access;
- preserve authored historical company/community content unless retention policy requires removal;
- preserve recognition/history;
- avoid hard-deleting identity relationships needed for audit.

## Migration rule

All production schema changes must be represented as migrations in Git.

No undocumented production-only Supabase schema state.


---

## Legacy migration baseline

The current migration baseline is documented in:

`docs/SCHEMA-BASELINE-LEGACY-MAPPING.md`

Key rules:

- shared Kalam People remains employee/person authority;
- Connect does not duplicate the full employee master;
- initial Connect identity is keyed by stable `kalam_app_id`, with canonical `person_id` added when verified;
- the 12 existing Webflow Connect categories seed the initial taxonomy;
- Category and Publication Type are separate concepts;
- legacy `Kalam Connects` items migrate into `publications` plus normalized people/category/media/action relationships;
- legacy fields without a final native destination are preserved losslessly in migration metadata;
- the preferred production boundary is a separate Kalam Connect application database/project consuming a minimal approved People projection.


---

## Publication behavior registry

PDISC-1B is locked in:

- `docs/PUBLICATION-TYPE-FIELD-MATRIX.md`
- `docs/decisions/PDISC-1B-PUBLICATION-TYPE-FIELD-MATRIX-LOCK.md`

Use separate concepts:

```text
publication_type
publication_subtype
category
```

Initial publication behavior types:

- story
- announcement
- recognition
- people_milestone
- event
- opportunity
- poll
- community_feature

Categories remain editorial taxonomy and do not directly define application behavior.

Prefer a controlled `publication_types` registry over a PostgreSQL enum so future approved types can be added without destructive type migrations.

Type-specific fields are stored in controlled `type_data` initially, while normalized relationships handle people, categories, media and actions.


---

## Magazine lifecycle, moderation and analytics

PDISC-1C is locked in:

- `docs/MAGAZINE-ANALYTICS-MODERATION-EDGE-CASES.md`
- `docs/decisions/PDISC-1C-MAGAZINE-ANALYTICS-MODERATION-LOCK.md`

Important distinctions:

- Archive = normal historical state.
- Withdrawn = exceptional removal from circulation.
- Hard deletion = exceptional privileged action.
- Published official content is revisioned.
- Timeline Shares resolve the current approved source revision.
- Archived source remains historically available by default.
- Withdrawn source is removed from normal member circulation.
- Magazine analytics are aggregate by default and do not provide a general viewer-surveillance list.
- Search authorization is checked against current audience rules.
