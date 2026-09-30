# Kalam Connect — Product Brief

**Status:** Product direction locked for planning  
**Owner:** Kalam  
**Repository:** `kalamcx/kalam-connect`  
**Production target:** `connect.kalam.cx`

## Product statement

Kalam Connect is a **private, authenticated internal magazine and social network for Kalam members**.

It combines curated internal communications with member participation so official company stories and everyday community interaction live in one product.

The product is not a public social network, a marketing website, a replacement for Kalam App, or an automation engine.

## Product promise

A Kalam member should be able to open one application and:

- see the newest important Kalam stories;
- discover recognition, birthdays, anniversaries, events, vacancies and announcements;
- follow the social timeline;
- publish appropriate member posts;
- react and comment;
- join communities;
- chat privately or in groups;
- view and maintain a member profile;
- receive relevant notifications;
- find people and content without exposing unnecessary employee data.

## Primary surfaces

### 1. Home / Magazine

The landing experience after authentication.

Purpose:
- editorially curated internal communication;
- latest official Kalam Connect publications;
- featured/hero story;
- category rails;
- recognition and people stories;
- announcements;
- upcoming events;
- vacancies/opportunities;
- selected community highlights.

This surface is curated rather than purely chronological.

### 2. Community / Timeline

The social feed.

Contains:
- member posts;
- official Connect posts;
- community posts where the member has access;
- reactions;
- threaded comments/replies;
- mentions;
- saved posts;
- media.

Default ranking can start with recency plus simple relevance; opaque algorithmic ranking is not required for MVP.

### 3. Communities

Spaces around departments, interests, projects, cohorts, locations or initiatives.

Community types:
- public-to-members;
- request-to-join;
- private/invite-only.

Each community can have:
- group profile/header;
- member list;
- group feed;
- rules;
- moderators/admins;
- optional group chat.

### 4. Messages

Private communication.

MVP:
- 1:1 conversations;
- small group conversations;
- message history;
- read state;
- attachments;
- basic search.

Later:
- typing/presence;
- richer reactions;
- message replies;
- voice/media enhancements.

### 5. Member Profile

A social representation of the verified Kalam person.

Company-controlled data and social/member-controlled data are separate.

Profile may show:
- name;
- verified avatar;
- department/team where appropriate;
- job title/role where appropriate;
- languages or approved public member fields;
- bio;
- interests;
- communities;
- member posts;
- recognitions;
- activity/privacy preferences.

## Staff surfaces

Authorized staff need:

- Magazine/Publication Manager;
- Campaign-linked publication queue;
- Draft / Review / Scheduled / Published / Archived views;
- community administration;
- moderation/report queue;
- member/access administration;
- events/vacancies management;
- notification controls;
- audit/activity log;
- automation health/status references without exposing raw n8n workflow internals.

## Content families

Native Connect publication types should support:

- story/article;
- announcement;
- recognition;
- Top Performers;
- birthday;
- anniversary;
- welcome/onboarding;
- event;
- vacancy/opportunity;
- poll/survey;
- community highlight;
- general post.

Types are presentation/behavior metadata around one publication model, not separate disconnected content systems.

## Non-goals

Kalam Connect does not own:

- Kalam employee master truth;
- cross-channel orchestration;
- n8n workflow implementation;
- Zoho Marketing Automation;
- public Kalam website CMS;
- public recruitment systems;
- SIA/SOLO product authority.

## Success principles

The product succeeds when it is:

- useful enough for members to return regularly;
- safe enough for private company/community communication;
- simple enough that staff can publish without technical work;
- structured enough that approved automations can create native content safely;
- independent enough that Connect can evolve without rebuilding upstream automation;
- measurable through engagement, reach, publishing and reliability metrics.
