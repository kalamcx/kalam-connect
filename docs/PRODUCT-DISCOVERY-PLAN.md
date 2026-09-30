# Kalam Connect — Product Discovery Plan

**Status:** ACTIVE  
**Date:** 30/09/2026

## Why this phase exists

Do not begin application implementation from the current high-level feature list.

Kalam Connect combines an editorial magazine, a social timeline, member profiles, communities, messaging, authentication, staff control and automation. If interaction rules are vague, implementation will create expensive rework.

The current priority is to define the product behavior completely enough that SOLO can execute without inventing product rules.

## Discovery principles

1. **Behavior before code.**
2. **One canonical object per concept.**
3. **Magazine and Timeline are related but not the same product surface.**
4. **Editorial control always wins on Magazine.**
5. **Social interaction happens through Timeline objects and member activity.**
6. **Tagged people must have deterministic projection behavior.**
7. **Every interaction has a visibility rule.**
8. **Member access derives from Kalam People + allowed email domains.**
9. **Design is a product system, not decoration after development.**
10. **Research informs decisions; we do not blindly clone another product.**

---

# Discovery workstreams

## PDISC-1 — Magazine editorial system

### PDISC-1A — Magazine Home & Builder — LOCKED

Frozen:
- homepage module architecture;
- visual Magazine Builder;
- Manual / Rule / Hybrid sourcing;
- editorial precedence;
- card family;
- reaction set;
- share behavior;
- comment-on-share behavior;
- tagged-person projections;
- sorting/filtering;
- scheduling/audience;
- versioned layout + rollback.

Canonical:
- `docs/MAGAZINE-EDITORIAL-MODEL.md`
- `docs/decisions/PDISC-1A-MAGAZINE-HOME-BUILDER-LOCK.md`

### PDISC-1B — Publication Types & Field Matrix — ACTIVE

Freeze:
- publication types;
- shared fields;
- type-specific fields;
- required/optional rules;
- media slots;
- people relationships;
- placement compatibility;
- automation/manual constraints.

### PDISC-1C — Magazine Analytics, Moderation & Edge Cases — PENDING

Freeze:
- analytics;
- moderation;
- publication edit/unpublish/archive consequences;
- restricted/deleted dependencies;
- archive/search edge behavior.

## PDISC-2 — Timeline/social graph

Define:
- authored posts;
- shared magazine publications;
- tagged posts;
- official projections;
- reactions;
- comments;
- replies;
- mentions;
- follows/connections if adopted;
- ranking;
- privacy;
- profile timeline projection;
- content removal/edit behavior.

Canonical detail:
`docs/SOCIAL-TIMELINE-MODEL.md`

## PDISC-3 — Profiles / settings / roles

Define:
- member profile anatomy;
- profile timelines/tabs;
- company-controlled vs member-controlled fields;
- settings;
- privacy;
- notifications;
- roles;
- capabilities;
- scoped community authority.

Canonical detail:
`docs/PROFILE-SETTINGS-ROLES.md`

## PDISC-4 — Membership & authentication

Define:
- Google auth;
- email auth;
- allowed domains;
- Kalam People eligibility;
- signup/provisioning;
- People DB backlink;
- joiner/mover/leaver;
- account recovery;
- session/security behavior.

Canonical detail:
`docs/AUTH-MEMBERSHIP-PLAN.md`

## PDISC-5 — Design & experience system

Define:
- product personality;
- mobile/desktop IA;
- navigation;
- magazine visual language;
- timeline visual language;
- profiles;
- communities;
- messaging;
- Control Center;
- motion;
- accessibility;
- KDS integration;
- prototypes and acceptance criteria.

Canonical detail:
`docs/DESIGN-EXPERIENCE-PLAN.md`

## PDISC-6 — Open-source/reference research

Research:
- mature community/social products;
- modern feed/profile experiences;
- messaging/community patterns;
- reusable code candidates;
- licenses;
- stack compatibility;
- what to borrow vs what to avoid.

Canonical detail:
`docs/OPEN-SOURCE-RESEARCH-2026-09-30.md`

## PDISC-7 — Complete function map

After PDISC-1 through PDISC-6:
- enumerate every member/staff/system action;
- define actors;
- define inputs;
- define object/state mutation;
- define visibility;
- define notification;
- define audit requirement;
- define permissions;
- define analytics event;
- define error/empty state.

Output:
`docs/FUNCTION-MAP.md`

## PDISC-8 — Prototype & decision freeze

Before implementation:
- mobile prototype;
- desktop prototype;
- magazine;
- timeline;
- profile;
- community;
- messages;
- Control Center;
- auth/onboarding;
- critical interaction walkthroughs.

Exit only when owner approves behavior + design.

---

# Discovery exit gate

Implementation may start only when:

- Magazine behavior is frozen.
- Timeline/share/tag/comment behavior is frozen.
- Profile behavior is frozen.
- Roles/capabilities are frozen.
- Auth/membership rules are frozen.
- Design direction and core screens are accepted.
- Open-source reuse decision is documented.
- Function map is complete.
- Data model is reconciled to final behavior.
- SOLO receives a versioned implementation handoff.

Until then:
**do not scaffold feature-heavy application code.**
