# Kalam Connect — Authentication, Roles & Security

## Membership rule

Kalam Connect is members-only.

No unrestricted public signup.

Eligibility derives from the shared Kalam People layer.

Email domain may assist verification but is not the membership authority.

## Target identity relationship

```text
shared Kalam person
      ↕ stable_person_id
Connect profile
      ↕
Supabase Auth user
```

## Provisioning options

Implementation may use:
- invite;
- OTP/magic link;
- Google login where appropriate;
- verified eligible email.

Regardless of login mechanism, account activation requires a matching eligible person record.

Not every Kalam member should be assumed to have a corporate-domain email.

## Joiner / mover / leaver

Joiner:
- eligible person appears upstream;
- account can be invited/activated;
- profile linked by stable person ID.

Mover:
- company-controlled fields refresh from People authority;
- member social history remains.

Leaver/inactive:
- access disabled/restricted;
- sessions revoked where practical;
- content/history retained per policy;
- memberships marked inactive where required.

## Global roles

Planning baseline:

- `member`
- `publisher`
- `moderator`
- `community_admin` (capability only; scope still required)
- `platform_admin`
- `super_admin`

HR/Marketing differences should normally be expressed through scoped capabilities rather than hard-coding department names throughout React.

## Capability examples

- profile.edit_own
- post.create
- post.edit_own
- comment.create
- community.join
- community.create
- community.manage
- message.send
- publication.create
- publication.review
- publication.publish
- publication.schedule
- moderation.review
- member.manage_access
- role.manage
- platform.manage

Model:

```text
role
→ capability
→ scope
→ database/server policy
```

## RLS principles

RLS is the security boundary, not frontend hiding.

Policies must cover:
- own profile edits;
- member-visible publications;
- audience/department/community restrictions;
- private community access;
- post/comment ownership;
- conversation participant access;
- private attachments;
- staff publishing;
- moderation;
- admin functions.

## Messaging security

Only participants can read/write conversation content.

Group membership changes must take effect for new content.

Sensitive privileged support access must be explicit, logged and narrowly scoped.

## Notification security

Do not permit normal authenticated users to insert arbitrary recipient notifications.

Preferred:

```text
valid action
→ trusted DB trigger/function/server action
→ notification
```

## Realtime security

Audit use of:
- postgres_changes;
- Broadcast;
- Presence.

If Broadcast/Presence/private channels are used, authorize topics by participant/community ownership.

## Storage security

Public:
- only assets intentionally public to all authenticated members where risk is acceptable.

Protected:
- private community files;
- message attachments;
- restricted staff assets.

Protected media should use RLS/signed access rather than permanent public URLs.

## Automation ingress

Automation/SOLO must call a server-side integration boundary.

Requirements:
- service authentication;
- version;
- source identity;
- capability allowlist;
- idempotency;
- approval/release state;
- audit receipt;
- rate limits;
- validation.

Never expose service-role/provider secrets to browser code.

## Moderation and member safety

Support:
- report;
- block;
- mute;
- remove/hide content;
- member restriction;
- community moderation;
- staff audit.

Moderation actions need reason/state and evidence.

## Privacy

Profiles expose only approved member fields.

Search/member pickers must not leak unnecessary:
- personal email;
- personal phone;
- private HR fields;
- source-system metadata.

Private messages must not be used for product analytics content inspection.

## Security acceptance before production

Must verify:
- no public signup bypass;
- inactive member access removal;
- RLS coverage;
- cross-community isolation;
- DM isolation;
- automation ingress authentication;
- idempotent publishing;
- notification spoof prevention;
- private storage access;
- role escalation prevention;
- audit integrity;
- secrets/env separation;
- rate limiting;
- backup/restore path.
