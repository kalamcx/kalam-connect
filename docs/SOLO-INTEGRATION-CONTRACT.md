# Kalam Connect ↔ SOLO Integration Contract

## Purpose

SOLO needs a stable, versioned interface to test, deploy and measure Kalam Connect without becoming Kalam Connect's product source of truth.

Kalam Connect exposes product capabilities.

SOLO owns the deployment/runtime adapter, environment configuration, contract tests, release evidence and rollback.

## Contract principles

- versioned;
- authenticated;
- least privilege;
- idempotent for retryable writes;
- auditable;
- provider-agnostic;
- no raw n8n workflow IDs in product code;
- no browser-to-n8n privileged path;
- explicit degraded/failure states.

## Capability manifest

Kalam Connect should expose a machine-readable manifest or equivalent documented contract with:

- product/version;
- environment;
- health/readiness;
- supported capabilities;
- API contract version;
- schema/migration version;
- dependency status;
- feature flags where needed.

## Proposed server capabilities

Names are planning identifiers, not frozen endpoint paths.

### connect.health.read
Returns:
- application status;
- database readiness;
- auth readiness;
- storage readiness;
- realtime readiness;
- version/release ID;
- degraded dependencies.

### connect.member.resolve
Input:
- stable person ID and/or approved identity lookup.

Output:
- member/profile ref;
- eligible state;
- minimal approved member data.

No unnecessary HR/private data.

### connect.publication.upsert
Trusted automation/staff capability.

Input:
- approved/preview package;
- campaign/content refs;
- publication payload;
- audience;
- schedule;
- idempotency key;
- correlation ID.

Output:
- publication ID;
- status;
- revision/version;
- preview/reference;
- execution receipt.

### connect.publication.release
Publishes/schedules an authorized publication.

Must verify:
- current object/version;
- release authority;
- approval reference;
- valid audience;
- assets ready.

### connect.publication.status
Read current publication/reconciliation state.

### connect.member.access.sync
Applies approved member eligibility/access changes from the shared people contract.

This must not allow arbitrary person creation from untrusted callers.

### connect.notification.system
Restricted system/staff notification capability.

Cannot be a generic user-controlled notification forge endpoint.

## Suggested HTTP boundary

One possible shape:

```text
/api/integrations/v1/health
/api/integrations/v1/members/resolve
/api/integrations/v1/publications
/api/integrations/v1/publications/{id}/release
/api/integrations/v1/publications/{id}/status
/api/integrations/v1/member-access/sync
```

Implementation may use Supabase Edge Functions or application server routes.

SOLO Gate 1 decides the runtime form.

## Standard request envelope

```json
{
  "contract_version": "1",
  "capability": "connect.publication.upsert",
  "correlation_id": "...",
  "idempotency_key": "...",
  "source": "solo|automation|staff",
  "actor": {
    "type": "service|user",
    "ref": "..."
  },
  "approval": {
    "required": true,
    "state": "approved",
    "reference": "..."
  },
  "payload": {}
}
```

## Standard success receipt

```json
{
  "ok": true,
  "contract_version": "1",
  "capability": "connect.publication.upsert",
  "correlation_id": "...",
  "receipt_id": "...",
  "object": {
    "type": "publication",
    "id": "...",
    "version": 1,
    "status": "review"
  }
}
```

## Standard failure shape

```json
{
  "ok": false,
  "correlation_id": "...",
  "code": "CONNECT_APPROVAL_REQUIRED",
  "retryable": false,
  "message": "..."
}
```

Do not expose internal stack traces or secrets.

## Error families

Suggested:
- CONNECT_UNAUTHORIZED
- CONNECT_FORBIDDEN
- CONNECT_CONTRACT_VERSION_UNSUPPORTED
- CONNECT_VALIDATION_FAILED
- CONNECT_MEMBER_NOT_ELIGIBLE
- CONNECT_APPROVAL_REQUIRED
- CONNECT_APPROVAL_STALE
- CONNECT_IDEMPOTENCY_CONFLICT
- CONNECT_PUBLICATION_NOT_FOUND
- CONNECT_ASSET_NOT_READY
- CONNECT_DEPENDENCY_DEGRADED
- CONNECT_INTERNAL_ERROR

## Events from Connect

Only emit automation-relevant events.

Examples:
- publication.review_ready;
- publication.published;
- publication.archived;
- moderation.escalated;
- member.access_changed;
- community.admin_request if later needed.

Do not stream every reaction/comment/message into n8n by default.

## Deployment handoff to SOLO

SOLO must receive:
- release artifact/version;
- migration version;
- environment variables contract;
- health endpoint;
- smoke-test suite;
- integration contract tests;
- rollback instructions;
- dependency matrix;
- test fixtures with no unnecessary production PII.

## SOLO acceptance

SOLO Gate 5/6 should verify:

- capability manifest;
- auth boundary;
- idempotency;
- approval enforcement;
- people identity mapping;
- publication create/update/release;
- failure/degraded behavior;
- migration compatibility;
- audit receipt;
- staging before production;
- rollback path.

## Separation rule

SOLO may deploy and test Kalam Connect, but must not silently redefine:
- Connect product semantics;
- member roles;
- content lifecycle;
- campaign authority;
- People source authority.

Changes to those belong in this repository and/or the appropriate upstream Workflow/Automation authority first.
