# Kalam Connect — Profiles, Settings, Roles & Users

## 1. Profile purpose

A profile represents a verified Kalam member inside the private network.

It combines:
- company-authoritative identity;
- member-controlled social identity;
- member activity.

---

# 2. Company-controlled fields

Read-only in Connect and synchronized from the shared People layer where approved:

- stable person ID;
- legal/preferred name as defined upstream;
- verified profile/photo reference;
- department/team;
- job title;
- approved location/site;
- approved language fields;
- membership/employment eligibility.

Connect must not overwrite source-of-truth employee fields.

---

# 3. Member-controlled fields

Potential:
- display preference where allowed;
- bio;
- interests;
- cover photo;
- social avatar override only if policy allows;
- pronouns if voluntarily supported;
- links/internal interests;
- profile theme/accent if adopted.

---

# 4. Profile layout

Suggested:

### Header
- cover;
- avatar;
- name;
- title/department;
- short bio;
- follow/message actions if permitted;
- profile stats.

### Tabs
- Timeline;
- Posts;
- Tagged;
- Media;
- Recognitions;
- Communities;
- About.

## Internal-public meaning

Profile information is visible only inside the authenticated Kalam Connect membership boundary unless a separate public-sharing feature is explicitly approved.

---

# 5. Member directory

Search/filter may include:
- name;
- department;
- team;
- title;
- language;
- community;
- interests.

Do not expose private phone/email/HR metadata unless explicitly required and approved.

---

# 6. Settings

Recommended groups:

### Account
- authentication methods;
- active sessions;
- logout all;
- account status;
- recovery.

### Profile
- bio;
- cover/avatar permitted edits;
- interests.

### Privacy
- profile projection controls;
- tagged-post controls;
- follow visibility if used;
- blocked members;
- muted members.

### Timeline
- preferred feed/tab;
- hidden content;
- followed people/communities.

### Notifications
Per event:
- reactions;
- comments;
- replies;
- mentions/tags;
- recognition;
- messages;
- community events;
- official announcements.

Channels:
- in-app;
- future email/push where adopted.

### Messages
- who may start a DM;
- read receipts if configurable;
- media/download preferences.

### Appearance
- light;
- dark;
- system;
- accessibility/reduced motion.

### Accessibility
- reduced motion;
- text scaling support;
- contrast options if needed.

---

# 7. Roles

Do not encode department names as security logic.

Recommended platform roles:

### Member
Normal social/member use.

### Editor
Create/edit official drafts, upload assets.

### Publisher
Approve/schedule/publish official content.

### Moderator
Review reports and moderate member content.

### Community Admin
Scoped to explicitly assigned communities.

### Member Admin
Manage Connect membership/access links subject to People authority.

### Design Admin
Manage safe Connect theme/template configuration.

### Analytics Viewer
Read approved analytics without publishing authority.

### Platform Admin
System configuration/integration administration.

### Super Admin
Full platform authority.

A user may hold multiple roles.

---

# 8. Capability model

Security model:

```text
role
→ capability
→ scope
→ RLS/server authorization
```

Examples:
- publication.create;
- publication.edit;
- publication.approve;
- publication.publish;
- magazine.layout.manage;
- media.upload;
- community.manage;
- moderation.review;
- analytics.read;
- member.access.manage;
- design.theme.manage;
- platform.roles.manage.

Community authority always includes community scope.

---

# 9. User lifecycle

States may include:
- eligible;
- invited;
- active;
- suspended;
- inactive/leaver.

Access and employment/member source truth remain separate.

Do not delete historical social identity just because access is disabled.

---

# 10. Profile backlink

On successful account provisioning, create a durable link between shared People identity and Connect profile.

Preferred pattern:
- shared integration relation/table rather than stuffing app fields into the canonical employee record where avoidable.

Example:
```text
people_app_links
- person_id
- app = kalam_connect
- profile_id
- profile_url
- status
- linked_at
```

Exact implementation depends on the shared Kalam People schema.
