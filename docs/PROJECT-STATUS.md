# Kalam Connect — Project Status

**Date:** 30/09/2026  
**Repository:** `kalamcx/kalam-connect`  
**Product:** Kalam Connect  
**Production target:** `connect.kalam.cx`

## Current stage

**PDISC — Product Behavior, Interaction & Design Discovery: ACTIVE**

KC0 produced the architecture skeleton, but the product is deliberately not implementation-ready yet.

PDISC-1A is now **LOCKED**:
- 100% staff-controlled Magazine composition/order/filter/schedule behavior;
- visual versioned Magazine Builder;
- Manual / Rule / Hybrid module sourcing;
- locked editorial precedence;
- initial card family;
- Like / Love / Celebrate / Support / Wow / Angry reactions;
- Magazine Share → Timeline discussion model;
- automatic official tagged-person projections.

PDISC-1B is now **LOCKED**:
- Category and Publication Type are separate.
- Eight initial native behavior types are fixed: story, announcement, recognition, people_milestone, event, opportunity, poll, community_feature.
- All 12 legacy Connect categories map into those types/subtypes.
- Universal and type-specific fields, media roles, people relationships, actions, placement compatibility, staff/automation ownership and lossless migration rules are defined.

PDISC-1C is now **LOCKED**:
- Archive, withdrawal and hard-delete semantics are fixed.
- Published official content uses revisions.
- Timeline Shares inherit source edit/archive/withdrawal state predictably.
- Inactive/unresolved people, categories, media, communities and actions have defined fallback/reconciliation behavior.
- Official-content reporting and moderation escalation are fixed.
- Reaction/share count semantics and Magazine analytics events are defined.
- Staff view analytics are aggregate by default rather than employee-surveillance lists.
- Search/archive and degraded-state behavior are fixed.

**PDISC-1 Magazine Editorial System is now COMPLETE / LOCKED.**

The active work now continues with **PDISC-2 — Timeline / Social Graph**.

Remaining discovery also includes:
- Timeline publishing/sharing/tagging behavior;
- automatic tagged-person projection to personal and internal-public profile timelines;
- profiles/settings/roles;
- Google + email authentication restricted to `kalam.cx` and `future-group.com` plus People eligibility;
- People↔Connect app linkage at provisioning;
- full design language/prototypes;
- open-source reference/reuse decisions;
- complete function map.

Implementation remains paused until the PDISC exit gate is approved.

PDISC-1A decision record:
`docs/decisions/PDISC-1A-MAGAZINE-HOME-BUILDER-LOCK.md`

PDISC-1B decision record:
`docs/decisions/PDISC-1B-PUBLICATION-TYPE-FIELD-MATRIX-LOCK.md`

PDISC-1C decision record:
`docs/decisions/PDISC-1C-MAGAZINE-ANALYTICS-MODERATION-LOCK.md`

## Locked product definition

Kalam Connect contains:

- Home / Magazine — curated official internal publications;
- Community — member/official social timeline;
- Communities — scoped groups with feeds and optional chat;
- Messages — 1:1 and group chat;
- Profiles — verified member identity/social profile;
- Search and Notifications;
- Control Center / Staff Admin — manual publishing, media management, preview/scheduling, moderation, design/theme controls, analytics and automation monitoring.

## Program boundary

- `kalamcx/kalam-connect` = Connect product authority.
- `kalamcx/solo` = deployment/integration test authority.
- `kalamcx/workflow` = workflow architecture authority.
- `kalamcx/automation` = n8n/agent implementation authority.
- Kalam People Database = shared people/member identity authority.

## Campaign decision

The missing cross-channel object is defined as an **Internal Communications Campaign**.

Connect does not own cross-channel orchestration.

Connect owns the native `publication` created from an approved campaign/content package.

Webflow and Zoho Marketing Automation are delivery adapters/provider systems, not Connect's content database.

## Data/security direction

- React/TypeScript application direction.
- Supabase Auth/Postgres/RLS/Storage/Realtime direction.
- member eligibility based on shared People data.
- no public unrestricted signup.
- RLS/trusted server boundary required.
- no direct privileged browser → n8n path.
- private community/message isolation required.
- native Connect content must not depend on Webflow CMS.

## Current next milestone

**PDISC-2 — Timeline / Social Graph**

SOLO must not begin broad Connect implementation yet.

After PDISC owner acceptance, proceed to **KC1 — Deployment Architecture & Repository Baseline** against SOLO Gate 1 / Gate 3.

## Known dependencies

- shared People stable identity contract;
- SOLO deployment architecture;
- future Workflow/Automation Internal Communications Campaign contract;
- KDS design-system availability for visual implementation.
- Control Center implementation per `docs/CONTROL-CENTER.md`.

## Current non-blocking note

This repository was observed as public during planning. No secrets were added.

Before sensitive implementation/configuration is committed, review whether the repository should be private.

## Canonical reading order

See root `AGENTS.md`.
