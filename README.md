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
- **Staff/Admin** — publishing, moderation, community/member administration and automation status.

The Community timeline is social content. Messages is the chat surface.

## Current stage

**KC0 — Product & Architecture Definition: COMPLETE**

**Next:** KC1 — Deployment Architecture & Repository Baseline, executed with SOLO.

Implementation has not started in this repository.

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
9. [Design System](docs/DESIGN-SYSTEM.md)
10. [Roadmap](docs/ROADMAP.md)
11. [Tasks](docs/TASKS.md)
12. [Project Status](docs/PROJECT-STATUS.md)
13. [Current Handoff](docs/CURRENT-HANDOFF.md)

## Security

Never commit secrets, service-role keys, OAuth credentials, provider tokens or production passwords.

This repository was observed as public during planning. Review visibility before sensitive implementation/configuration is added.
