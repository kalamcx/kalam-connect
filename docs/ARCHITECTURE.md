# Kalam Connect — Target Architecture

## Architectural principle

Kalam Connect is a separate product that consumes shared Kalam capabilities through versioned contracts.

```text
Kalam App / People authority
          ↓
Shared Kalam People Database
          ↓
   member eligibility/profile link
          ↓
     Kalam Connect
          ↕
      SOLO adapter
          ↕
 Workflow / Automation
          ↕
Webflow / Zoho MA / other providers
```

## Ownership

### Kalam Connect owns
- native member application;
- magazine publications;
- social posts/comments/reactions;
- profiles;
- communities and memberships;
- private/group messaging;
- Connect notifications;
- Connect moderation;
- Connect-specific audit state;
- Connect-specific roles/capabilities.

### Shared People layer owns
- canonical Kalam person identity;
- employment/member eligibility;
- company-owned identity fields;
- stable source identifier.

### Workflow Design owns
- approved business-process definition;
- approval/handoff rules;
- cross-system campaign lifecycle.

### Automation owns
- n8n workflows/agents;
- provider execution;
- deterministic orchestration;
- runtime evidence.

### SOLO owns
- deployment/integration adapter;
- environments;
- release gates;
- QA;
- telemetry;
- rollback;
- contract verification.

## Application stack direction

Preferred application model:

- React + TypeScript;
- Supabase Postgres;
- Supabase Auth;
- Supabase RLS;
- Supabase Realtime where justified;
- Supabase Storage;
- server-side Edge Functions/API boundary for privileged integrations.

Production domain:
`connect.kalam.cx`.

Hosting/deployment platform is finalized by SOLO Gate 1. Webflow Cloud remains a viable candidate but is not made authoritative by this document.

## No Webflow CMS dependency

Native Kalam Connect magazine/feed content should live in Connect/Supabase.

Webflow may remain:
- a public website channel;
- a temporary/legacy publishing adapter;
- a visual design/deployment tool where approved.

Webflow CMS must not be required for Connect to function.

## Browser/server boundary

Browser:
- authenticated member UI;
- anon/public-safe config only;
- normal member mutations subject to RLS.

Trusted server/API:
- automation ingress;
- publication release;
- privileged moderation;
- audit writes;
- notification fanout;
- provider callbacks;
- service credentials.

## Environments

Required:

```text
LOCAL / DEV
→ TEST / isolated integration
→ STAGING
→ PRODUCTION
```

Each environment requires:
- distinct URLs;
- distinct secrets;
- controlled data;
- explicit provider targets;
- release identity;
- migration version;
- smoke tests;
- rollback path.

Production employee/member data must not be casually copied into test environments.

## Integration strategy

SOLO should not expose raw n8n workflow internals to Kalam Connect.

Preferred pattern:

```text
Kalam Connect capability/API
        ↕
SOLO contract adapter
        ↕
Automation capability manifest
        ↕
n8n/provider systems
```

Every side-effecting integration should support:
- version;
- correlation ID;
- idempotency key;
- actor/source;
- authority/risk;
- approval state;
- execution receipt;
- failure/degraded state.

## Realtime

Use realtime only where member experience materially benefits.

Good candidates:
- messages;
- unread counts;
- notifications;
- selected feed/comment updates.

Do not automatically use Broadcast/Presence for everything.

Private realtime channels require explicit authorization.

## Storage

Logical buckets may include:
- avatars;
- covers;
- publication-media;
- member-post-media;
- message-attachments;
- community-media;
- event-assets.

Private community/message files must not use public URLs that bypass authorization.

## Observability

Must capture:
- frontend errors;
- auth failures;
- RLS/authorization failures;
- Edge Function/API failures;
- message delivery failures;
- publication automation failures;
- provider/automation degraded states;
- migration/release identifiers.

Do not log private message bodies unnecessarily.

## Resilience

Kalam Connect should remain usable if Automation or an external provider is unavailable.

Core member actions use Connect/Supabase directly.

External automation failures should degrade into:
- pending/retry;
- visible staff exception;
- execution receipt/failure reference.

They must not make the entire social product unavailable.
