# AGENTS.md — Kalam Connect

## Purpose

This repository is the product and implementation authority for **Kalam Connect**, Kalam's authenticated member-only magazine, social community, and messaging platform.

Production target: `connect.kalam.cx`.

## Authority boundaries

Read these repositories as upstream authorities when their domains are involved:

- `kalamcx/solo` — deployment/integration test authority, environments, release gates, QA, telemetry, rollback.
- `kalamcx/workflow` — approved business/workflow architecture and system handoffs.
- `kalamcx/automation` — n8n/agent implementation and runtime evidence.
- Kalam People Database — shared employee/member identity source.
- Native providers — authority for their own delivery/analytics data.

Kalam Connect must not silently redefine upstream workflow, automation, people, or provider truth.

## Product model

Kalam Connect has five primary member surfaces:

1. **Home / Magazine** — curated official internal stories and campaigns.
2. **Community / Timeline** — member and official posts with reactions and threaded comments.
3. **Communities** — department/interest/project communities with group feeds.
4. **Messages** — 1:1 and group chat.
5. **Profile** — member identity, social profile, activity, connections and preferences.

Staff/admin surfaces support publication, moderation, communities, campaigns, members and audit.

## Important distinction

The Community timeline is not chat. It is the social feed.

Messages is the private/group chat surface.

## Automation boundary

Cross-channel campaign orchestration belongs upstream in Workflow Design/Automation/SOLO.

Kalam Connect owns the native Connect publication created from an approved campaign/content package.

Preferred relationship:

```text
Workflow Design
  → Automation / approved campaign package
  → SOLO integration adapter
  → Kalam Connect native publication
  → optional delivery adapters:
       - Webflow
       - Zoho Marketing Automation
       - other approved channels
```

Do not make Webflow CMS the Kalam Connect source of truth.

## Identity boundary

Member access is based on an eligible active record in the shared Kalam People layer, not public self-signup and not email domain alone.

Target relationship:

```text
Supabase Auth
→ Connect profile
→ shared person identity
→ stable Kalam person ID
```

Company-owned employee attributes remain read-only inside Connect.

## Security

- Never commit secrets or credentials.
- Browser code receives public-safe configuration only.
- RLS/trusted server functions are the authorization boundary.
- Service-role/provider credentials are server-side only.
- Never allow ordinary clients to forge notifications, audit records, approvals, or privileged publication actions.
- Private community and messaging data must use strict membership/participant policies.
- Keep historical content when employment/access becomes inactive unless retention policy explicitly requires deletion.

## Execution rules

1. Preserve product authority and repo documentation before large implementation.
2. Complete PDISC behavior/design gates before implementation milestones in `docs/ROADMAP.md`.
3. Do not treat visual prototypes or temporary provider adapters as product truth.
4. Every automation-facing capability must be versioned, idempotent where applicable, auditable, and return a correlation/execution receipt.
5. External publishing/sending remains human-gated unless a later approved policy explicitly changes it.
6. Update `docs/PROJECT-STATUS.md`, `docs/TASKS.md`, and `docs/CURRENT-HANDOFF.md` after each milestone.
7. Do not start the next milestone without the prior exit gate being satisfied.

## Canonical repository docs

Read in this order:

1. `AGENTS.md`
2. `docs/PRODUCT-BRIEF.md`
3. `docs/PRODUCT-EXPERIENCE.md`
4. `docs/ARCHITECTURE.md`
5. `docs/DATA-MODEL.md`
6. `docs/AUTH-SECURITY.md`
7. `docs/AUTOMATION-CONTENT-MODEL.md`
8. `docs/SOLO-INTEGRATION-CONTRACT.md`
9. `docs/PRODUCT-DISCOVERY-PLAN.md`
10. `docs/MAGAZINE-EDITORIAL-MODEL.md`
11. `docs/PUBLICATION-TYPE-FIELD-MATRIX.md`
12. `docs/MAGAZINE-ANALYTICS-MODERATION-EDGE-CASES.md`
13. `docs/SOCIAL-TIMELINE-MODEL.md`
14. `docs/PROFILE-SETTINGS-ROLES.md`
15. `docs/AUTH-MEMBERSHIP-PLAN.md`
16. `docs/DESIGN-EXPERIENCE-PLAN.md`
17. `docs/OPEN-SOURCE-RESEARCH-2026-09-30.md`
18. `docs/FUNCTION-MAP.md`
19. `docs/DESIGN-SYSTEM.md`
20. `docs/CONTROL-CENTER.md`
21. `docs/ROADMAP.md`
22. `docs/TASKS.md`
23. `docs/PROJECT-STATUS.md`
24. `docs/CURRENT-HANDOFF.md`
