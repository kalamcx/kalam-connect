# Kalam Connect

Kalam Connect is Kalam's **authenticated member-only internal magazine, social community and messaging platform**.

Production target: `connect.kalam.cx`.

## Product

Kalam Connect combines:

- **Home / Magazine** — curated official Kalam stories, recognition, announcements, events and opportunities;
- **Community / Timeline** — member and official posts with reactions and comments;
- **Communities** — department/interest/project groups with scoped feeds and optional chat;
- **Messages** — private 1:1 and group conversations;
- **Profiles** — verified member identity and social profile;
- **Search & Notifications**;
- **Control Center / Staff Admin** — manual publishing, media uploads, preview/scheduling, design controls, moderation, analytics and automation monitoring.

The Community timeline is social content. Messages is the chat surface.

## Current stage

**PDISC — Product Behavior, Interaction & Design Discovery: ACTIVE**

KC0 established the architecture skeleton, but implementation is intentionally paused while Magazine, Timeline, tagging, profiles, settings, roles, authentication, design and open-source reuse are fully mapped.

**Do not start feature implementation yet.**

**PDISC-1A Magazine Home & Builder is locked. PDISC-1B Publication Types & Field Matrix is locked.** Current active step: **PDISC-1C — Magazine Analytics, Moderation & Edge Cases**.

After PDISC owner acceptance, SOLO resumes with KC1 — Deployment Architecture & Repository Baseline.

## Program ownership

- `kalamcx/kalam-connect` — Kalam Connect product/application authority.
- `kalamcx/solo` — deployment, integration testing, environments, QA, release and rollback.
- `kalamcx/workflow` — approved business/workflow architecture.
- `kalamcx/automation` — n8n/agent implementation and runtime evidence.
- shared Kalam People layer — member/person identity authority.

## Campaign model

The cross-channel business object is an **Internal Communications Campaign**.

Workflow/Automation coordinate the campaign.

Kalam Connect owns the native **publication** created from the approved campaign/content package.

Webflow and Zoho Marketing Automation are delivery/provider adapters, not Kalam Connect's application database.

## Architecture direction

- React + TypeScript;
- Supabase Auth/Postgres/RLS/Storage/Realtime;
- member eligibility from shared Kalam People data;
- server-side trusted integration boundary;
- versioned/idempotent SOLO/Automation contracts;
- no public unrestricted signup;
- no privileged browser → n8n path;
- no long-term Webflow CMS dependency for native Connect content.

Final deployment/runtime choice is confirmed by SOLO KC1/Gate 1.

## Start here

Read in order:

1. [AGENTS.md](AGENTS.md)
2. [Product Brief](docs/PRODUCT-BRIEF.md)
3. [Product Experience](docs/PRODUCT-EXPERIENCE.md)
4. [Architecture](docs/ARCHITECTURE.md)
5. [Data Model](docs/DATA-MODEL.md)
6. [Auth & Security](docs/AUTH-SECURITY.md)
7. [Campaign & Automation Model](docs/AUTOMATION-CONTENT-MODEL.md)
8. [SOLO Integration Contract](docs/SOLO-INTEGRATION-CONTRACT.md)
9. [Product Discovery Plan](docs/PRODUCT-DISCOVERY-PLAN.md)
10. [Magazine Editorial Model](docs/MAGAZINE-EDITORIAL-MODEL.md)
11. [Social Timeline Model](docs/SOCIAL-TIMELINE-MODEL.md)
12. [Profiles, Settings, Roles](docs/PROFILE-SETTINGS-ROLES.md)
13. [Auth & Membership Plan](docs/AUTH-MEMBERSHIP-PLAN.md)
14. [Design & Experience Plan](docs/DESIGN-EXPERIENCE-PLAN.md)
15. [Open-Source Research](docs/OPEN-SOURCE-RESEARCH-2026-09-30.md)
16. [Function Map](docs/FUNCTION-MAP.md)
17. [Design System](docs/DESIGN-SYSTEM.md)
18. [Control Center](docs/CONTROL-CENTER.md)
19. [Roadmap](docs/ROADMAP.md)
20. [Tasks](docs/TASKS.md)
21. [Project Status](docs/PROJECT-STATUS.md)
22. [Current Handoff](docs/CURRENT-HANDOFF.md)

## Security

Never commit secrets, service-role keys, OAuth credentials, provider tokens or production passwords.

This repository was observed as public during planning. Review visibility before sensitive implementation/configuration is added.
