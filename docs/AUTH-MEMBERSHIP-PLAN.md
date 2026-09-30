# Kalam Connect — Authentication & Membership Plan

## Locked product requirement

Only eligible Kalam/Future Group members may create/access Kalam Connect accounts.

Allowed email domains:
- `kalam.cx`
- `future-group.com`

Supported sign-in methods:
- Google authentication;
- email authentication.

Domain alone is not sufficient.

A matching eligible active person in the shared Kalam People Database is also required.

---

# 1. Recommended authentication flow

```text
Google OAuth OR Email verification
          ↓
normalize email
          ↓
allowed domain check
          ↓
lookup shared Kalam People
          ↓
eligible active person?
     ├─ no → reject / access-request path
     └─ yes
          ↓
create/resolve Supabase Auth user
          ↓
create Connect profile
          ↓
link stable person ID
          ↓
write Connect app-link metadata
          ↓
authenticated member session
```

## Google

Use Supabase Google OAuth.

Still run server-side eligibility checks.

A Google account using the correct-looking email must not bypass the People Database eligibility check.

## Email

Preferred first option:
- email OTP/magic-link verification.

This avoids a separate password-support burden.

If password authentication is later required, it needs explicit password/reset/security planning.

---

# 2. Signup rejection

Reject when:
- domain is not allowed;
- no People record exists;
- People record is ineligible/inactive;
- identity conflict exists;
- account is suspended.

Provide a clear non-sensitive message and an access-request/help route.

Do not reveal private HR status details.

---

# 3. Supabase enforcement

Use a server-side/auth hook gate rather than UI validation alone.

Supabase currently supports a **Before User Created Hook** that can reject signups, including by email domain. The final hook should also verify the Kalam People eligibility contract.

Frontend domain checks are UX only.

---

# 4. Profile provisioning

On first successful eligibility/auth:

- create or resolve profile;
- attach stable person ID;
- copy only approved display fields;
- set account state;
- create app-link metadata;
- apply default Member role;
- record provisioning audit event.

Provisioning must be idempotent.

---

# 5. Shared People backlink

Requirement:
the People layer should be able to discover the member's Connect profile.

Preferred:
`people_app_links` or equivalent integration relation.

Fields conceptually:
- person_id;
- app;
- profile_id;
- profile_url;
- account_state;
- linked_at;
- updated_at.

This avoids making Connect-specific fields part of every employee source record unless the People schema owner chooses that design.

---

# 6. Joiner / mover / leaver

Joiner:
- appears eligible upstream;
- can authenticate/provision.

Mover:
- department/title/etc. update from People;
- Connect content/history remains.

Leaver/inactive:
- block new sessions;
- revoke active sessions where feasible;
- preserve historical authorship/recognition;
- profile becomes inactive according to presentation policy.

---

# 7. Identity conflict

Handle:
- duplicate emails;
- changed work email;
- person record merge;
- account already linked to another auth ID.

Never solve identity conflict automatically by creating a second profile.

---

# 8. Security tests

Required before production:
- non-allowed domain rejected;
- allowed domain but no People record rejected;
- inactive People record rejected;
- Google sign-in cannot bypass eligibility;
- email sign-in cannot bypass eligibility;
- profile provisioning idempotent;
- duplicate auth cannot create duplicate profile;
- leaver access removed;
- existing authored content preserved;
- app-link back-reference correct.
