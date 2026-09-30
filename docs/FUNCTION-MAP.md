# Kalam Connect — Function Map

**Status:** Discovery baseline — expand during prototype review.

Each function must eventually define:
- actor;
- capability;
- object;
- input;
- state change;
- visibility;
- notification;
- audit;
- analytics event;
- error states.

---

# A. Magazine / Editorial

## Member
- open Magazine Home;
- browse configured sections;
- filter where enabled;
- open publication;
- react/change/remove reaction;
- share publication to Timeline;
- add share caption;
- open tagged member;
- save/bookmark where enabled;
- view archive/search.

## Editor/Publisher
- create publication;
- edit;
- choose type/template;
- upload/select media;
- tag one/many people;
- select category;
- select audience;
- schedule;
- expire/archive;
- place in Magazine modules;
- reorder modules;
- pin items;
- configure rule-based collection;
- preview device/audience;
- submit review;
- approve;
- publish;
- unpublish/archive;
- view revision/audit.

---

# B. Timeline / Social

## Member — feed
- open For You;
- open Following;
- open Latest;
- open Communities feed;
- refresh;
- navigate to source post/publication/profile/community.

## Member — create
- create original post;
- add text;
- upload image/gallery/video/approved attachment;
- add safe link;
- tag people;
- mention people;
- choose All Members or eligible Community;
- publish.

## Member — share/distribute
- share Magazine publication with optional commentary;
- repost member post without commentary;
- undo repost;
- quote member post with commentary.

## Member — interact
- react/change/remove reaction;
- comment;
- reply one level;
- Like comment/reply;
- edit own comment;
- delete own comment;
- hide comment on own post;
- turn comments on/off;
- bookmark where enabled.

## Member — social graph
- follow;
- unfollow;
- mute;
- unmute;
- block;
- unblock.

## Member — tagging/profile control
- hide tagged projection from own profile;
- remove own tag from member-authored post;
- report/request correction for official tagged publication.

## Member — own post lifecycle
- edit text/tags/alt text;
- view Edited state;
- soft-delete post.

Member cannot after publish:
- widen/change destination;
- change post kind/source;
- replace/add/remove primary media in MVP.

## Member — safety
- report post/share/quote/comment/profile;
- hide/collapse blocked content according to shared-Community rules.

## System
- build deterministic For You feed;
- build chronological Following/Latest feeds;
- project structured Tags to tagged member Timeline/profile;
- distinguish Tag from Mention;
- enforce source-audience intersection on share/repost/quote;
- suppress blocked/muted interactions;
- remove Reposts when source is deleted/moderated;
- render unavailable source for Quote when ordinary source delete permits quote commentary to remain;
- create trusted notifications;
- preserve revision/moderation evidence;
- fall back to Latest if ranking is unavailable.

## Moderator
- triage report;
- hide/remove/restore content;
- lock comments;
- restrict posting/commenting;
- escalate member access issue;
- preserve audit reason.

---

# C. Profiles

## Member
- view profile;
- edit allowed fields;
- upload allowed avatar/cover;
- view Timeline;
- view Posts;
- view Tagged;
- view Recognitions;
- view Media;
- view Communities;
- Follow/Unfollow if model adopted;
- Message;
- hide tagged projection;
- manage block/mute.

## System
- synchronize company fields;
- preserve profile link to People identity;
- deactivate access without deleting history.

---

# D. Communities

## Member
- discover communities;
- view;
- join;
- request join;
- leave;
- publish;
- react/comment;
- view members;
- open community chat if enabled;
- report content.

## Community Admin
- create/configure where authorized;
- approve membership;
- invite/remove member;
- set rules;
- pin/moderate posts;
- assign scoped moderator;
- manage cover/accent.

---

# E. Messages

## Member
- open conversation list;
- start eligible DM;
- create group;
- send;
- edit/delete according to policy;
- attach media/file;
- react/reply if adopted;
- read receipts;
- search own conversations;
- manage participants where authorized;
- mute conversation;
- report conversation/member.

## System
- authorize participant access;
- realtime deliver;
- unread counts;
- attachment protection;
- retention rules.

---

# F. Notifications

## Member
- view;
- mark read;
- mark all read;
- navigate to source;
- configure notification categories.

## System
Generate trusted notifications for:
- reaction;
- comment/reply;
- tag/mention;
- recognition;
- Magazine share interaction;
- message;
- community invite/request;
- official announcement;
- system/access event.

---

# G. Search

Search:
- people;
- Magazine publications;
- Timeline posts;
- communities;
- events/opportunities.

Filters/visibility must respect authorization.

---

# H. Authentication / Membership

## User
- Google sign-in;
- email sign-in;
- verify email;
- recover access;
- sign out;
- manage sessions.

## System
- enforce allowed domain;
- verify People eligibility;
- provision profile idempotently;
- create People↔Connect link;
- refresh company fields;
- disable inactive member;
- prevent duplicate identity.

---

# I. Control Center

## Publishing
- draft;
- preview;
- approval;
- scheduling;
- placement;
- publish/archive.

## Media
- upload;
- validate;
- metadata;
- search;
- reuse;
- see usages.

## Magazine Builder
- add/remove modules;
- reorder;
- configure layout;
- configure query;
- manual pin/order;
- audience;
- timing;
- preview.

## Moderation
- reports;
- hide/remove;
- restrict;
- restore where policy permits;
- record reason.

## Community
- create/manage;
- member requests;
- roles.

## Design
- select approved theme/tokens/templates;
- preview;
- no unrestricted CSS for routine staff.

## Monitoring
- content analytics;
- community analytics;
- auth/member health;
- automation delivery;
- failures/retry;
- audit log.

---

# J. Automation / SOLO

Trusted capabilities:
- member resolve;
- publication upsert;
- publication release;
- publication status;
- member access sync;
- integration health.

Automation must use the same objects humans manage in Control Center.

---

# K. Decisions still open

Must be frozen before implementation:
- follow vs no explicit follow graph;
- member-post repost/quote-share;
- exact reaction set/icons;
- comment edit/delete policy;
- post edit history;
- tag removal/review rules;
- DM initiation policy;
- message edit/delete/retention;
- community creation rights;
- profile visibility details;
- analytics definitions;
- stories/reels: currently **not included** unless a later product decision adds them.
