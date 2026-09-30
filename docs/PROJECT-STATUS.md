# Kalam Connect — Project Status

**Date:** 30/09/2026  
**Repository:** `kalamcx/kalam-connect`  
**Product:** Kalam Connect  
**Production target:** `connect.kalam.cx`

## Current stage

**KC0 — Product & Architecture Definition: COMPLETE**

The repository now contains the canonical planning baseline for Kalam Connect as a member-only internal magazine/social/community/messaging product.

Implementation has not started in this repository.

## Locked product definition

Kalam Connect contains:

- Home / Magazine — curated official internal publications;
- Community — member/official social timeline;
- Communities — scoped groups with feeds and optional chat;
- Messages — 1:1 and group chat;
- Profiles — verified member identity/social profile;
- Search and Notifications;
- Staff/Admin — publishing, moderation, community/member administration and automation status.

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

**KC1 — Deployment Architecture & Repository Baseline**

SOLO should execute KC1 against its Gate 1 / Gate 3 program architecture.

## Known dependencies

- shared People stable identity contract;
- SOLO deployment architecture;
- future Workflow/Automation Internal Communications Campaign contract;
- KDS design-system availability for visual implementation.

## Current non-blocking note

This repository was observed as public during planning. No secrets were added.

Before sensitive implementation/configuration is committed, review whether the repository should be private.

## Canonical reading order

See root `AGENTS.md`.
