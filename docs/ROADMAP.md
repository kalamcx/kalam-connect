# Kalam Connect — Implementation Roadmap

## Operating rule

One milestone at a time.

Every milestone ends with:
- evidence;
- tests;
- documentation update;
- explicit exit-gate result.

SOLO may execute the deployment/integration work, but this repository remains Kalam Connect product authority.

---

## KC0 — Product & Architecture Definition

**Status: COMPLETE**

Deliverables:
- product brief;
- information architecture;
- target architecture;
- logical data model;
- auth/security model;
- campaign/content model;
- SOLO integration contract;
- design direction;
- roadmap/tasks/handoff.

Exit gate:
- repository contains enough authority for implementation planning without chat history.

---

## PDISC — Product Behavior, Interaction & Design Discovery

**Status: ACTIVE**

Implementation is paused during this discovery gate.

### PDISC-1 — Magazine editorial system

#### PDISC-1A — Magazine Home & Builder — COMPLETE / LOCKED
- [x] Freeze module/page-builder behavior.
- [x] Freeze card variants.
- [x] Freeze reaction behavior.
- [x] Freeze Magazine Share → Timeline behavior.
- [x] Freeze comment visibility model.
- [x] Freeze tagged-person projection rules.
- [x] Freeze editorial sort/filter/schedule/audience controls.
- [x] Freeze versioned Magazine layout + rollback.
- [x] Record product decision lock.

Canonical:
- `docs/MAGAZINE-EDITORIAL-MODEL.md`
- `docs/decisions/PDISC-1A-MAGAZINE-HOME-BUILDER-LOCK.md`

#### PDISC-1B — Publication Types & Field Matrix — COMPLETE / LOCKED
- [x] Freeze publication types.
- [x] Define universal publication fields.
- [x] Define type-specific fields.
- [x] Define required/optional fields.
- [x] Define media roles by type.
- [x] Define tagged-person relationship types.
- [x] Define placement compatibility by type.
- [x] Define automation/manual creation constraints.
- [x] Separate Category from Publication Type.
- [x] Map all 12 legacy Connect categories.
- [x] Record decision lock.

Canonical:
- `docs/PUBLICATION-TYPE-FIELD-MATRIX.md`
- `docs/decisions/PDISC-1B-PUBLICATION-TYPE-FIELD-MATRIX-LOCK.md`

Initial native types:
- story
- announcement
- recognition
- people_milestone
- event
- opportunity
- poll
- community_feature

#### PDISC-1C — Magazine Analytics, Moderation & Edge Cases — COMPLETE / LOCKED
- [x] Freeze publication/reaction/share analytics.
- [x] Freeze report/moderation behavior for official content.
- [x] Freeze edit/unpublish/archive consequences.
- [x] Freeze behavior when source media/person/community becomes unavailable.
- [x] Freeze reaction/share behavior on archived/restricted content.
- [x] Freeze Magazine search/archive edge cases.
- [x] Freeze archive vs withdrawn vs hard-delete semantics.
- [x] Freeze published revision behavior and analytics privacy boundary.
- [x] Record decision lock.

Canonical:
- `docs/MAGAZINE-ANALYTICS-MODERATION-EDGE-CASES.md`
- `docs/decisions/PDISC-1C-MAGAZINE-ANALYTICS-MODERATION-LOCK.md`

**PDISC-1 Magazine Editorial System: COMPLETE / LOCKED**

### PDISC-2 — Timeline/social graph — ACTIVE
- [ ] Freeze post types.
- [ ] Freeze tagging.
- [ ] Freeze repost/quote-share decision.
- [ ] Freeze reaction/comment/reply behavior.
- [ ] Decide Follow vs no explicit graph.
- [ ] Freeze public/internal profile timeline behavior.
- [ ] Freeze edit/delete/moderation behavior.

### PDISC-3 — Profiles/settings/roles
- [ ] Freeze profile anatomy/tabs.
- [ ] Freeze company vs member-editable fields.
- [ ] Freeze settings groups.
- [ ] Freeze platform roles.
- [ ] Freeze capability/scoping model.

### PDISC-4 — Auth/membership
- [ ] Freeze Google + email auth UX.
- [ ] Enforce kalam.cx + future-group.com domains.
- [ ] Require eligible Kalam People record.
- [ ] Freeze account provisioning.
- [ ] Freeze People↔Connect app link.
- [ ] Freeze joiner/mover/leaver behavior.

### PDISC-5 — Design
- [ ] Freeze mobile navigation.
- [ ] Freeze desktop navigation.
- [ ] Accept Magazine Home visual prototype.
- [ ] Accept Timeline prototype.
- [ ] Accept Profile prototype.
- [ ] Accept Communities prototype.
- [ ] Accept Messages prototype.
- [ ] Accept Control Center prototype.
- [ ] Accept KDS mapping.

### PDISC-6 — Open-source/reuse
- [ ] Review shortlisted projects.
- [ ] Score UX/stack/security/test/license/KDS fit.
- [ ] Decide reference-only vs selective reuse.
- [ ] Record rejected architectural directions.

### PDISC-7 — Function map
- [ ] Expand every member/staff/system function with permissions, state, visibility, notifications, audit, analytics and failure states.

### PDISC-8 — Prototype & owner freeze
- [ ] Walk critical end-to-end flows.
- [ ] Resolve open decisions.
- [ ] Owner accepts behavior/design.
- [ ] Reconcile final data model.
- [ ] Issue versioned SOLO implementation handoff.

**Exit gate:** owner-approved product behavior + design + function map. Only then proceed to KC1.

---

## KC1 — Deployment Architecture & Repository Baseline

**Owner:** SOLO + Kalam Connect

Work:
- confirm framework/runtime;
- choose deployment platform;
- define local/test/staging/production;
- define CI/CD;
- define secrets strategy;
- define Supabase project/environment boundary;
- define migration workflow;
- define health/readiness surface;
- make repository private before sensitive code/config is added if still public;
- establish app scaffold only after architecture is approved.

Do not:
- start feature-heavy UI;
- bind browser directly to n8n;
- create provider secrets in frontend.

Exit gate:
- SOLO Gate 1 + Gate 3 compatible deployment architecture approved.

---

## KC2 — Shared People & Authentication Foundation

Dependencies:
- shared Kalam People contract available;
- stable person ID confirmed.

Work:
- connect read-safe People projection;
- establish Supabase Auth;
- link auth user ↔ Connect profile ↔ stable person ID;
- member eligibility check;
- invite/login flow;
- joiner/mover/leaver behavior;
- inactive access test;
- profile bootstrap.

Exit gate:
- only eligible Kalam members can authenticate;
- no public signup bypass;
- historical identity survives access disable.

---

## KC3 — Database, RLS, Storage & Security Foundation

Work:
- migrations for core tables;
- roles/capabilities;
- RLS;
- trusted notification creation;
- audit log;
- protected storage;
- realtime authorization;
- rate-limit strategy;
- integration service auth;
- idempotency receipts.

Exit gate:
- security test matrix passes before member/social features expand.

---

## KC4 — Application Shell & KDS Foundation

Work:
- responsive app shell;
- navigation;
- Home / Community / Communities / Messages / Notifications / Profile / Search;
- staff/admin navigation by capability;
- KDS token integration;
- primitives;
- theme foundation;
- loading/empty/error states;
- accessibility baseline.

Exit gate:
- responsive shell and component foundation accepted on phone/tablet/desktop.

---

## KC5 — Magazine / Home

Work:
- publication model;
- categories;
- featured story;
- latest posts;
- recognition/people rail;
- announcements;
- events/opportunities;
- publication detail;
- audience/visibility;
- schedule/expiry;
- related people/community projections.

Exit gate:
- staff can create a native draft and members can consume published magazine content safely.

---

## KC6 — Community Timeline & Social Interaction

Work:
- member composer;
- member posts;
- feed;
- reactions;
- threaded comments;
- mentions;
- bookmarks;
- report post/comment;
- media;
- visibility rules;
- basic ranking/recency.

Exit gate:
- verified members can safely create and interact with social content.

---

## KC7 — Profiles, Directory, Search & Notifications

Work:
- member profile;
- company vs member-editable fields;
- people directory;
- profile posts/recognitions;
- unified search MVP;
- in-app notifications;
- notification preferences;
- block/mute;
- trusted notification fanout.

Exit gate:
- members can discover people/content without leaking restricted data.

---

## KC8 — Communities

Work:
- public/request/private community types;
- membership requests;
- community roles;
- community rules;
- community feed;
- community member list;
- community moderation;
- optional community chat switch/contract.

Exit gate:
- private community isolation tested and scoped administration verified.

---

## KC9 — Messaging

Work:
- direct conversations;
- group conversations;
- participant management;
- message send/read;
- unread counts;
- attachments;
- basic message search;
- reporting/safety path;
- realtime delivery;
- retention/privacy policy.

Exit gate:
- non-participants cannot read or mutate conversation content or attachments.

---

## KC10 — Control Center / Staff Publishing, Moderation & Admin

Canonical operations specification:

`docs/CONTROL-CENTER.md`

Work:
- Control Center overview;
- publication manager;
- drafts/review/scheduled/published/archive;
- event/vacancy management where Connect owns presentation;
- community admin;
- moderation queue;
- report resolution;
- member access controls;
- staff activity log;
- automation receipt/status views;
- native Media Library;
- publication preview lab;
- design/theme/template controls within KDS governance;
- content/community/automation monitoring;
- manual publishing fallback when Automation/SOLO is unavailable.

Exit gate:
- daily staff operations can be performed without direct DB access, Supabase Studio, n8n, or Webflow Designer.

---

## KC11 — Campaign / SOLO / Automation Integration

Dependencies:
- Workflow Design internal campaign contract;
- Automation capability manifest;
- SOLO runtime contract adapter.

Work:
- versioned integration API;
- connect.publication.upsert;
- connect.publication.release;
- publication status/reconciliation;
- campaign/content refs;
- multi-person recognition;
- approved asset handling;
- idempotency;
- partial failure/degraded state;
- delivery receipts;
- Zoho MA adapter reconciliation upstream;
- Webflow adapter treated as optional delivery, not Connect authority.

Exit gate:
- an approved campaign package can create/update/release a native Connect publication repeatedly without duplicates.

---

## KC12 — Reliability, Analytics & Production Readiness

No major feature expansion.

Work:
- unit tests;
- integration/contract tests;
- E2E;
- performance budgets;
- accessibility QA;
- security review;
- backup/restore;
- retention;
- observability;
- error monitoring;
- automation degradation behavior;
- analytics;
- mobile QA;
- load/realtime testing;
- migration rehearsal;
- rollback rehearsal.

Critical E2E:
- login/eligibility;
- magazine read;
- create post;
- react/comment;
- search profile;
- join/request private community;
- DM/group message isolation;
- staff publication;
- recognition multi-person;
- moderation;
- automation publication idempotency;
- inactive member access;
- logout.

Exit gate:
- production release candidate approved.

---

## KC13 — Staging & Production Deployment

Work:
- isolated staging;
- production configuration;
- final migrations;
- auth redirect/domain;
- `connect.kalam.cx`;
- smoke tests;
- monitoring;
- rollback point;
- launch validation.

Exit gate:
- production operational with no critical security/reliability findings.

---

## After launch

Prioritize based on evidence:
- richer feed relevance;
- comment reactions;
- enhanced messaging;
- presence/typing;
- PWA/offline;
- richer member discovery;
- community events;
- recommendation/personalization;
- richer staff campaign analytics;
- additional notification channels.

Do not add complexity merely because a public social platform has it.
