# Kalam Connect — Product Experience & Information Architecture

## Navigation

Recommended primary member navigation:

```text
Home
Community
Communities
Messages
Notifications
Profile
Search
```

Staff/admin navigation appears only by capability.

## Home / Magazine experience

Home should feel like an internal digital magazine, not a dashboard.

Suggested structure:

1. Featured story / campaign
2. Latest from Kalam
3. Recognition & People
4. Announcements
5. Community highlights
6. Upcoming events
7. Opportunities / vacancies
8. Explore categories

Editorial controls:
- feature/unfeature;
- pin;
- schedule;
- expiry;
- category;
- audience;
- related people;
- related community;
- campaign reference.

## Community timeline

The Community tab is the member social timeline.

Post composer supports:
- text;
- image/gallery;
- link;
- poll;
- document where allowed;
- mention;
- community selection where permitted.

Post card supports:
- author;
- timestamp;
- audience/community;
- content/media;
- reaction summary;
- comment count;
- save/bookmark;
- report.

Initial reactions should be intentionally small rather than copying every public network.

Recommended MVP:
- Like;
- Celebrate;
- Support.

## Comments

- threaded replies at least one level deep;
- reactions to comments can be deferred;
- edit/delete own comment;
- moderator removal with audit reason;
- mention member;
- report comment.

## Communities

Community screen:
- header/cover;
- description;
- privacy state;
- rules;
- admins/moderators;
- membership action;
- feed;
- members;
- optional chat tab.

A user's global role does not automatically grant administration of every community.

## Messages

Messaging is separate from the timeline.

MVP:
- conversation list;
- unread counts;
- 1:1 messages;
- group messages;
- read state;
- attachments;
- participant controls.

Security:
- only conversation participants can read/write;
- removed participants cannot access new messages;
- group admins do not gain access to unrelated DMs;
- privileged support/debug access requires explicit policy and audit.

## Profiles

Profile tabs can include:
- About;
- Posts;
- Recognitions;
- Communities.

Company-owned fields are read-only.

User-editable fields may include:
- bio;
- interests;
- preferred display details;
- social avatar/cover where policy permits;
- notification/privacy preferences.

## Search

Unified search should eventually cover:
- people;
- publications/posts;
- communities;
- events;
- vacancies.

MVP can ship people + posts + communities first.

## Notifications

Member-facing in-app notifications:
- reaction;
- comment/reply;
- mention;
- follow/connections if enabled;
- message;
- community invite/request result;
- event reminder;
- official announcement;
- recognition;
- staff/system notice.

Notification generation must be trusted/server-side.

## Accessibility & responsive behavior

Target:
- keyboard-accessible navigation/composer/modals;
- visible focus;
- semantic headings;
- adequate contrast;
- alt text support;
- reduced-motion support;
- responsive phone/tablet/desktop layouts;
- touch targets suitable for mobile;
- no critical feature requiring hover.

## Experience states

Every major screen needs:
- loading;
- empty;
- partial/degraded;
- permission denied;
- unavailable;
- error;
- offline/retry where relevant.

## Product analytics

Measure at minimum:
- active members;
- magazine reach;
- publication views;
- feed engagement;
- reaction/comment rate;
- community participation;
- message adoption;
- notification interaction;
- search usage;
- publication turnaround;
- moderation volume;
- automation-created publication success/failure.

Analytics must not expose private message content.
