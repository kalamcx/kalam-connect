# Kalam Connect — Control Center / Studio

## Purpose

Kalam Connect requires an internal **Control Center** for authorized staff.

The member-facing application is the social/magazine experience.

The Control Center is the operational workspace used to:

- manage the visual/design system;
- upload and manage media;
- create and edit publications manually;
- receive automation-created drafts;
- preview;
- review/approve;
- schedule;
- publish/unpublish/archive;
- target audiences;
- manage categories;
- manage communities;
- moderate member content;
- monitor member activity/engagement;
- inspect campaign/channel delivery status;
- inspect automation failures/degraded states;
- review audit history.

A staff member must be able to operate Kalam Connect manually even if SOLO/n8n is temporarily unavailable.

---

# 1. Control Center navigation

Recommended information architecture:

```text
Overview

Content
├── Magazine Builder
├── Publications
├── Drafts
├── Scheduled
├── Media Library
├── Categories
├── Events
└── Opportunities

Community
├── Member Posts
├── Comments
├── Reports
├── Communities
└── Members

Campaigns
├── Campaign Queue
├── Connect Deliveries
├── Email Deliveries
├── Webflow Deliveries
└── Failures / Reconciliation

Design
├── Design Tokens
├── Themes
├── Components
├── Publication Templates
├── Category Styles
└── Preview Lab

Analytics
├── Overview
├── Publications
├── Community
├── Communities
└── Engagement

System
├── Access & Roles
├── Automation Status
├── Audit Log
├── Storage
└── Settings
```

Only authorized capabilities should reveal each section.

---

# 2. Overview dashboard

The Control Center landing page should answer:

- What needs attention?
- What is scheduled?
- What was published recently?
- What failed?
- What is getting engagement?
- Are there moderation issues?
- Is automation healthy?

Suggested widgets:

### Publishing
- Drafts awaiting review
- Scheduled today
- Scheduled this week
- Recently published
- Expiring soon

### Automation
- Campaign packages received
- Successful Connect deliveries
- Failed/degraded deliveries
- Pending retries
- Last successful automation receipt

### Community
- Active members
- New member posts
- Comments/reactions today
- Reports awaiting moderation
- Communities requiring approval

### System
- Auth status
- People sync freshness
- Storage status
- Realtime status
- application release/version

---

# 3. Magazine Builder

The Control Center includes a visual Magazine Builder governed by the locked PDISC-1A model.

Staff can:

- add/remove/show/hide Magazine modules;
- drag/reorder modules;
- choose layout and card presets;
- configure Manual / Rule / Hybrid sourcing;
- build filters;
- choose sorting;
- pin/exclude/manual-order publications;
- set audience;
- set module/placement schedule;
- choose approved theme/accent;
- preview desktop/tablet/mobile;
- preview by audience;
- save a draft layout;
- publish a new layout version;
- rollback to a previous layout version.

Editorial precedence is fixed by:

`docs/decisions/PDISC-1A-MAGAZINE-HOME-BUILDER-LOCK.md`

Automation cannot silently alter the live Magazine layout, Hero, pins or manual ordering.

---

# 4. Manual publication workflow

Manual publishing must use the same native publication model as automation.

Do not maintain a separate manual publishing system.

```text
New Publication
→ choose content type
→ add content
→ add media
→ select category
→ select related people
→ select related community
→ select audience
→ choose placements
→ preview
→ save draft
→ review/approve
→ publish now OR schedule
→ publication appears on selected Connect surfaces
→ analytics + audit begin
```

## Publication form

### Basics
- publication type;
- title;
- summary;
- body/content;
- category;
- tags where supported.

### People
- related employee/member;
- multiple members supported;
- relationship type:
  - recognition;
  - birthday;
  - anniversary;
  - welcome;
  - mention;
  - author/feature.

### Media
- cover/main creative;
- thumbnail;
- gallery;
- video;
- document;
- link preview.

### Audience
- all eligible members;
- departments;
- communities;
- selected members;
- optional future custom audience.

### Placement
A single publication may appear in multiple Connect experiences:

- Magazine home;
- Community timeline;
- Community page;
- related member profile;
- Events section;
- Opportunities section.

Placement must not create duplicate publication records.

### Timing
- publish now;
- schedule;
- expiry/archive date.

### Status
- Draft
- Review
- Scheduled
- Published
- Archived

### Source
Display origin:
- Manual;
- SOLO;
- Automation;
- campaign reference;
- source event/request.

---

# 5. Manual upload / Media Library

The Control Center needs a native Media Library.

## Supported asset classes

- images;
- videos;
- documents;
- publication covers;
- thumbnails;
- member/profile images where policy allows;
- community covers;
- event assets.

## Upload flow

```text
Upload
→ validate file
→ optimize/scan
→ classify asset
→ add alt text
→ add title/description
→ add ownership/source
→ add related campaign/publication/person if applicable
→ store
→ reusable media record
```

## Media metadata

Recommended:
- media ID;
- file name;
- mime/type;
- file size;
- dimensions/duration;
- storage bucket/path;
- alt text;
- title;
- source;
- uploaded by;
- uploaded at;
- related campaign;
- related publication;
- related person/community;
- privacy/access state;
- usage count.

## Media rules

- never replace verified employee photography with AI-generated faces;
- optimize images before delivery;
- protect private-message/private-community media;
- preserve attribution/source where required;
- allow staff to see where an asset is used;
- avoid duplicate uploads when the same approved asset is reused.

---

# 6. Preview system

Every official publication should have a preview before release.

Preview modes:

- Magazine desktop
- Magazine tablet
- Magazine mobile
- Community feed
- Profile projection
- Community projection
- Notification preview

Optional later:
- email adaptation preview;
- Webflow delivery preview.

The preview should use the real KDS/components, not a disconnected fake mockup.

---

# 7. Publishing controls

Authorized publishers should have:

### Draft controls
- edit;
- duplicate;
- delete if policy permits;
- submit for review.

### Review controls
- approve;
- request changes;
- disregard/archive;
- compare revision.

### Release controls
- publish now;
- schedule;
- reschedule;
- cancel schedule;
- unpublish/withdraw where policy allows;
- archive.

All privileged publication actions create audit entries.

---

# 8. Design Control System

Kalam Connect should not require developers for normal visual adjustments.

## Three layers

### Layer A — Kalam Design System / shared foundations

Authority for:
- core typography;
- brand colors;
- semantic colors;
- spacing;
- radii;
- borders;
- shadows;
- motion;
- breakpoints;
- foundational components.

This should come from KDS rather than being recreated uniquely inside Connect.

### Layer B — Connect theme configuration

Connect-specific design controls:

- light/dark theme;
- magazine surface/background;
- feed surface/background;
- text hierarchy;
- category accent mapping;
- card radius;
- publication aspect ratios;
- content width;
- hero behavior;
- avatar size families;
- magazine density;
- feed density.

These should map to approved tokens, not arbitrary raw CSS values.

### Layer C — Editorial templates

Staff-selectable publication layouts:

- Feature story;
- Standard article;
- Announcement;
- Recognition;
- Top Performers;
- Birthday;
- Anniversary;
- Welcome;
- Event;
- Vacancy;
- Poll.

Each template defines:
- supported fields;
- media slots;
- typography role;
- category color behavior;
- placement behavior;
- responsive layout.

Staff may choose templates without editing application code.

---

# 9. Design administration UX

Recommended Design section:

## Design Tokens
Read-only for most staff.

Super Admin/design authority may update approved Connect token mappings.

## Themes
- light;
- dark;
- category/topic variations.

## Components
Visual catalogue:
- buttons;
- cards;
- badges;
- inputs;
- avatars;
- post cards;
- story cards;
- message bubbles;
- navigation.

## Publication Templates
Preview/edit approved configurable options.

## Category Styles
Map:
`category → approved accent token → icon/visual behavior`.

## Preview Lab
Render sample content across:
- desktop;
- tablet;
- phone;
- light/dark;
- publication types.

---

# 10. Design-system governance

Do not expose unrestricted CSS editing to ordinary staff.

Changes fall into three classes:

### Safe content/editorial changes
Staff can control:
- copy;
- media;
- category;
- placement;
- scheduling;
- supported template choice.

### Safe theme configuration
Authorized design/admin users can control approved token selections.

### Structural design-system changes
Require versioned KDS/application work:
- new tokens;
- new component APIs;
- navigation architecture;
- layout primitives;
- global spacing system;
- new template structures.

These go through Git/release management.

---

# 11. Monitoring / Analytics

Monitoring is split into four views.

## A. Content performance

Per publication:
- views/reach;
- unique viewers;
- reactions;
- reaction rate;
- comments;
- comment rate;
- bookmarks;
- click-through where measurable;
- engagement rate;
- audience reach;
- related campaign.

## B. Community health

- active members;
- posting members;
- commenting members;
- reactions;
- most active communities;
- community growth;
- unanswered/reported content;
- moderation volume.

## C. Messaging health

Only metadata/technical metrics:
- active conversations;
- messages sent;
- delivery failures;
- unread counts;
- realtime errors.

Do not expose/read private message bodies in product analytics.

## D. Automation / campaign operations

Per campaign/delivery:
- campaign ref;
- content package ref;
- Connect publication status;
- Zoho MA status;
- Webflow status if used;
- last attempt;
- execution receipt;
- correlation ID;
- failure code;
- retry state.

This gives staff a human-readable operational layer without exposing raw n8n internals.

---

# 12. Automation + manual control relationship

Automation must produce the same objects that humans manage.

Preferred:

```text
Automation creates draft
→ staff sees it in Control Center
→ staff edits if needed
→ staff approves
→ staff publishes/schedules
```

or, where workflow policy already permits release:

```text
approved automation package
→ native Connect publication
→ Control Center shows receipt/status
```

Manual fallback:

```text
automation unavailable
→ staff creates publication manually
→ native Connect publication
→ audit marks origin = manual
→ later reconciliation can link it to campaign if needed
```

The platform must never stop internal publishing merely because automation is offline.

---

# 13. Monitoring states

Every external/integration object should have:

- healthy;
- pending;
- running;
- awaiting approval;
- scheduled;
- completed;
- degraded;
- failed;
- retrying;
- blocked.

Do not represent every problem as a generic red error.

---

# 14. Staff roles

Suggested capabilities:

### Publisher
- create/edit drafts;
- upload assets;
- submit for review.

### Publishing Manager
- approve;
- schedule;
- publish;
- archive;
- control editorial placement.

### Moderator
- reports;
- remove/hide content;
- member restrictions within policy.

### Community Admin
- scoped community management.

### Design Admin
- Connect theme/template configuration;
- cannot arbitrarily bypass KDS governance.

### Platform Admin
- roles/access;
- system configuration;
- integrations;
- operational monitoring.

### Super Admin
- full platform authority.

---

# 15. Control Center acceptance

Before production, staff must be able to complete without DB access:

1. configure and publish a Magazine layout version;
2. create manual publication;
3. upload image;
3. select verified employee;
4. preview;
5. save draft;
6. approve;
7. schedule;
8. publish;
9. confirm Home/feed placement;
10. monitor engagement;
11. inspect automation origin/receipt;
12. see failed delivery and retry/escalation state;
13. moderate a reported post;
14. manage a community;
15. view audit history.

If these require Supabase Studio, SQL, Webflow Designer or n8n for daily work, the Control Center is incomplete.
