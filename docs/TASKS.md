# PDISC — Product Discovery / Behavior Freeze
- [ ] Freeze Magazine module builder and editorial controls.
- [ ] Freeze Magazine card/reaction set.
- [ ] Freeze Magazine Share → Timeline model.
- [ ] Freeze comment visibility on shared Magazine posts.
- [ ] Freeze tagged-person automatic projection.
- [ ] Freeze Timeline post/share/repost behavior.
- [ ] Decide Follow model.
- [ ] Freeze Profile tabs and settings.
- [ ] Freeze roles/capabilities/scopes.
- [ ] Freeze Google + email auth rules.
- [ ] Freeze People eligibility + Connect backlink model.
- [ ] Complete open-source reuse scoring.
- [ ] Complete mobile/desktop design prototypes.
- [ ] Expand Function Map to permissions/state/visibility/audit/analytics/error states.
- [ ] Owner accepts product behavior/design.
- [ ] Issue SOLO implementation handoff.

# Kalam Connect — Execution Checklist

## KC0 — Product & Architecture
- [x] Define member-only product.
- [x] Define Home/Magazine.
- [x] Define Community timeline.
- [x] Separate Messages from timeline.
- [x] Define Communities.
- [x] Define Profile.
- [x] Define staff/admin surfaces.
- [x] Define logical data model.
- [x] Define auth/roles/security.
- [x] Define campaign/publication boundary.
- [x] Define SOLO integration contract.
- [x] Define design direction.
- [x] Define roadmap.

## KC1 — Deployment architecture
- [ ] Confirm repository visibility and make private before sensitive implementation if required.
- [ ] Confirm framework/runtime.
- [ ] Confirm hosting/deployment platform.
- [ ] Define DEV/TEST/STAGING/PRODUCTION.
- [ ] Define Supabase environment/project strategy.
- [ ] Define secret management.
- [ ] Define migrations.
- [ ] Define CI checks.
- [ ] Define health/readiness endpoint.
- [ ] Define release ID/version.
- [ ] Define rollback.
- [ ] Record SOLO Gate 1/Gate 3 acceptance.

## KC2 — People/Auth
- [ ] Confirm stable shared person ID.
- [ ] Confirm minimum People projection fields.
- [ ] Implement people resolver.
- [ ] Implement Supabase Auth.
- [ ] Implement profile bootstrap.
- [ ] Block unrestricted signup.
- [ ] Implement eligibility check.
- [ ] Implement inactive/leaver access behavior.
- [ ] Test member without corporate-domain email if eligible.
- [ ] Test invalid/non-member rejection.

## KC3 — Security/data
- [ ] Create migrations.
- [ ] Create roles/capabilities.
- [ ] Add RLS to all protected tables.
- [ ] Add private storage policies.
- [ ] Add trusted notification generation.
- [ ] Add audit log.
- [ ] Add integration receipts.
- [ ] Add service auth.
- [ ] Add idempotency.
- [ ] Review realtime channel authorization.
- [ ] Add rate-limit strategy.
- [ ] Run authorization abuse tests.

## KC4 — Shell/KDS
- [ ] App shell.
- [ ] Responsive navigation.
- [ ] Magazine route.
- [ ] Community route.
- [ ] Communities route.
- [ ] Messages route.
- [ ] Notifications route.
- [ ] Profile route.
- [ ] Search route.
- [ ] Staff/admin gated routes.
- [ ] KDS tokens.
- [ ] Core primitives.
- [ ] Loading/empty/error states.
- [ ] Accessibility baseline.

## KC5 — Magazine
- [ ] Publications migration/model.
- [ ] Publication type metadata.
- [ ] Categories.
- [ ] Feature/pin/schedule/expiry.
- [ ] Publication detail.
- [ ] Home hero.
- [ ] Latest rail.
- [ ] Recognition rail.
- [ ] Announcements.
- [ ] Events.
- [ ] Opportunities.
- [ ] Audience rules.
- [ ] Multi-person publication links.

## KC6 — Community timeline
- [ ] Composer.
- [ ] Member post.
- [ ] Feed.
- [ ] Media.
- [ ] Reactions.
- [ ] Comments.
- [ ] Replies.
- [ ] Mentions.
- [ ] Bookmarks.
- [ ] Report.
- [ ] Visibility policy.
- [ ] Feed pagination/performance.

## KC7 — Profiles/search/notifications
- [ ] Profile view/edit.
- [ ] Company-field read-only boundary.
- [ ] People directory.
- [ ] Profile posts.
- [ ] Profile recognitions.
- [ ] Search people/posts/communities.
- [ ] Notifications.
- [ ] Notification preferences.
- [ ] Block.
- [ ] Mute.
- [ ] Notification spoof-prevention test.

## KC8 — Communities
- [ ] Community CRUD.
- [ ] Public/request/private.
- [ ] Membership.
- [ ] Scoped admin/moderator.
- [ ] Rules.
- [ ] Group feed.
- [ ] Members.
- [ ] Moderation.
- [ ] Private isolation tests.

## KC9 — Messages
- [ ] Direct conversation.
- [ ] Group conversation.
- [ ] Participants.
- [ ] Send/edit/delete policy.
- [ ] Read state.
- [ ] Unread counts.
- [ ] Attachments.
- [ ] Realtime.
- [ ] Search.
- [ ] Report/safety.
- [ ] Participant isolation tests.

## KC10 — Control Center / Staff Admin
- [ ] Control Center overview dashboard.
- [ ] Publication manager.
- [ ] Review state.
- [ ] Schedule.
- [ ] Archive.
- [ ] Moderation queue.
- [ ] Member access UI.
- [ ] Community admin.
- [ ] Event/vacancy admin.
- [ ] Activity log.
- [ ] Automation receipt/status UI.
- [ ] Native Media Library.
- [ ] Upload validation/metadata/alt text.
- [ ] Publication Preview Lab.
- [ ] Light/dark and approved theme controls.
- [ ] Publication template selector.
- [ ] Category-style mapping.
- [ ] Content analytics.
- [ ] Community analytics.
- [ ] Automation/delivery monitoring.
- [ ] Manual publication fallback with origin/audit tracking.
- [ ] Verify daily operation requires no direct DB/n8n/Webflow access.

## KC11 — SOLO/Automation
- [ ] Capability manifest.
- [ ] Health/readiness.
- [ ] Service authentication.
- [ ] connect.member.resolve.
- [ ] connect.publication.upsert.
- [ ] connect.publication.release.
- [ ] connect.publication.status.
- [ ] connect.member.access.sync.
- [ ] Contract versioning.
- [ ] Correlation IDs.
- [ ] Idempotency.
- [ ] Approval version check.
- [ ] Multi-person recognition.
- [ ] Asset readiness.
- [ ] Partial failure/degraded status.
- [ ] Delivery receipt reconciliation.
- [ ] Contract tests in SOLO.

## KC12 — Production readiness
- [ ] Unit suite.
- [ ] Integration suite.
- [ ] Contract suite.
- [ ] Critical E2E suite.
- [ ] Accessibility QA.
- [ ] Mobile/tablet QA.
- [ ] Performance budget.
- [ ] Security review.
- [ ] Backup/restore test.
- [ ] Retention policy.
- [ ] Observability.
- [ ] Automation outage test.
- [ ] People upstream outage test.
- [ ] Realtime/load test.
- [ ] Migration rehearsal.
- [ ] Rollback rehearsal.

## KC13 — Launch
- [ ] Staging acceptance.
- [ ] Production configuration.
- [ ] DNS/domain.
- [ ] Auth redirects.
- [ ] Production migration.
- [ ] Smoke test.
- [ ] Monitoring.
- [ ] Rollback point.
- [ ] Owner acceptance.
