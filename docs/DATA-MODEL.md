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
`draft → review → scheduled → published → archived`.

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
Threaded post/publication comments.

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
