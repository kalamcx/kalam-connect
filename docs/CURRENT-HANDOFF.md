# Kalam Connect — Current Handoff to SOLO

**Date:** 30/09/2026  
**Handoff:** KC0 complete → KC1 ready

## What SOLO is receiving

A complete product/architecture baseline in `kalamcx/kalam-connect`:

- product definition;
- information architecture;
- data model;
- identity/security model;
- campaign/publication model;
- automation boundary;
- integration contract;
- design direction;
- milestone roadmap;
- execution checklist.

## SOLO's next job

Run **KC1 — Deployment Architecture & Repository Baseline** as part of SOLO's deployment gates.

SOLO should determine:

1. final runtime/framework;
2. deployment platform;
3. DEV/TEST/STAGING/PRODUCTION topology;
4. Supabase environment strategy;
5. network/request boundaries;
6. secret management;
7. CI/CD;
8. migrations;
9. health/readiness;
10. release/rollback model.

Do not start broad feature implementation before KC1 exits.

## Required program boundary

```text
Kalam Connect
= product/application authority

SOLO
= deployment, integration testing, environment, release and rollback authority

Workflow
= business-process architecture authority

Automation
= n8n/agent implementation authority

Kalam People
= member/person identity authority
```

## Product surfaces SOLO must preserve

```text
Home / Magazine
Community / Timeline
Communities
Messages
Notifications
Profile
Search
Control Center / Staff Admin
```

The timeline is social content. Messages is chat.

## Critical implementation rules

- member-only access;
- no public signup bypass;
- stable person identity from shared People layer;
- company fields separate from social profile fields;
- no raw n8n workflow inventory in the product model;
- no browser-to-n8n privileged path;
- no Webflow CMS dependency for native Connect content;
- cross-channel campaign is upstream;
- Connect publication is the native channel projection;
- human/approved release policy remains enforceable;
- automation writes are versioned/idempotent/auditable;
- private community/message RLS is a production gate.

## Automation handoff

SOLO Gate 5 should use:

`docs/SOLO-INTEGRATION-CONTRACT.md`

Campaign/content semantics:

`docs/AUTOMATION-CONTENT-MODEL.md`

Expected initial Connect capabilities:

- health/readiness;
- member resolve;
- publication upsert;
- publication release;
- publication status;
- member access sync.

## First vertical slice recommendation

After KC1–KC3 foundations, implement one end-to-end slice before broad UI expansion:

```text
eligible member
→ login
→ magazine home
→ staff/automation creates recognition draft
→ related member resolved from People
→ human approval/release
→ publication appears on Home + Community
→ member reacts/comments
→ notification generated
→ audit/integration receipt preserved
```

This tests identity, publishing, social interaction, notifications and automation in one coherent path.

## Exit from planning

The next agent should not re-plan the product from scratch.

Read `AGENTS.md` in this repository and proceed from KC1 unless the owner changes the product direction.


## Control Center requirement

Daily Marketing/Community operations must be possible from the native Connect Control Center without direct access to Supabase Studio, n8n, or Webflow Designer.

Canonical specification:

`docs/CONTROL-CENTER.md`

This includes:
- manual publication creation;
- media upload/library;
- preview;
- review/approval;
- schedule/publish/archive;
- design/theme/template controls within KDS governance;
- content/community analytics;
- moderation;
- automation/campaign delivery status;
- manual fallback when automation is unavailable.
