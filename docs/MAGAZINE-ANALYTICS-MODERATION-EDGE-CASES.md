# PDISC-1C — Magazine Analytics, Moderation & Edge Cases

**Decision date:** 30/09/2026  
**Status:** LOCKED  
**Scope:** Official Magazine/publication analytics, moderation, revisions, withdrawal/archive behavior and failure cases

## Core principles

1. Magazine remains editor-controlled.
2. Analytics informs staff; analytics does not silently reorder Magazine content.
3. Published content is versioned and auditable.
4. Archive preserves history.
5. Withdrawal protects accuracy, privacy and safety.
6. Hard deletion is exceptional.
7. Timeline Shares reference the canonical publication and therefore inherit source availability/state.
8. Historical people recognition is preserved when employment/access changes.
9. Member analytics must not become employee surveillance.
10. Operational/system logs and product engagement analytics are separate concerns.

---

# 1. Publication lifecycle — final behavior

Official publication states:

```text
draft
→ review
→ scheduled
→ published
→ archived

published/scheduled
→ withdrawn
```

## Draft

- staff/automation may edit according to ownership/revision rules;
- invisible to members;
- may be permanently deleted if it has never been published and has no required audit/dependency record.

## Review

- frozen review revision;
- material changes after submission create a new revision and reopen approval;
- invisible to members except authorized preview.

## Scheduled

- approved publication awaiting release;
- authorized publisher may change schedule;
- material content changes return it to review unless an approved policy explicitly says otherwise.

## Published

- visible only to authorized audience;
- may be placed in Magazine modules, official Timeline, profile projections or specialized surfaces;
- interactions follow type/publication configuration.

## Archived

Normal historical state.

Archived means:
- removed from active Magazine placement unless an Archive/History module explicitly includes it;
- still accessible by direct link, archive/search and profile/recognition history when audience permits;
- existing Timeline Shares continue to resolve;
- reactions/shares remain by default unless disabled;
- expired actions such as apply/register become disabled.

Archive is not a moderation action.

## Withdrawn

Exceptional removal state for:
- materially incorrect content;
- privacy issue;
- security issue;
- policy/moderation issue;
- publication released in error.

Withdrawn means:
- remove from Magazine modules;
- remove official Timeline placement;
- remove profile/category/community discovery projections;
- exclude from normal search/archive discovery;
- disable new reactions;
- disable new shares;
- disable actions;
- preserve publication/revision/audit data for authorized staff.

Existing Timeline Shares:
- leave normal member feeds;
- stop rendering original publication content/media;
- show only a minimal unavailable/withdrawn state where needed for author/history;
- lock new comments/replies/reactions;
- may be hidden entirely when privacy/security requires it.

Do not use Archive when content must stop circulating.

---

# 2. Hard deletion

Hard deletion is allowed only for:

### Normal case
- unpublished draft;
- no downstream references;
- no required audit/evidence dependency.

### Exceptional published-content case
Requires Platform Admin/Super Admin plus a recorded reason such as:
- legal/privacy erasure requirement;
- severe security exposure;
- prohibited content that must not remain in normal application storage.

Normal published content should use Archive or Withdraw, not delete.

When hard deletion is required:
- preserve only the minimum permitted audit tombstone/reference;
- remove sensitive content/media;
- reconcile Timeline Shares and cached projections.

---

# 3. Revision model

Every published official publication is revisioned.

Recommended `publication_revisions` fields:
- publication_id;
- revision_number;
- snapshot;
- change_summary;
- changed_by;
- source;
- created_at;
- approval_ref;
- published_at.

## Minor edits

Examples:
- spelling;
- punctuation;
- alt text;
- non-material formatting.

Behavior:
- create revision;
- update live publication;
- preserve audit;
- renewed approval is not mandatory if publishing policy permits.

## Material edits

Examples:
- title meaning changes;
- people added/removed;
- recognition claim changes;
- dates/deadlines;
- vacancy requirements;
- audience;
- significant body changes;
- source asset replacement that changes meaning.

Behavior:
- create new revision;
- require review/approval before new revision goes live;
- current approved revision remains live until replacement is approved unless unsafe;
- if unsafe, withdraw current publication first.

Member UI can show `Updated` plus the latest meaningful update timestamp.

Do not expose internal staff diffs to normal members.

---

# 4. Timeline Share behavior after source changes

Timeline Share stores:
- canonical publication reference;
- member commentary;
- author/audience;
- social interaction on that share.

It does not duplicate the official publication body.

### Source edited
- rich preview resolves the current approved publication revision;
- member commentary remains unchanged;
- meaningful source updates can show an `Updated` indicator.

### Source archived
- Share continues to resolve;
- preview remains available;
- existing/new share interactions continue unless disabled.

### Source withdrawn
- Share stops showing official content/media;
- leaves normal feeds;
- new reactions/comments/replies/shares are disabled;
- audit/history is preserved according to withdrawal reason.

### Source hard deleted
- Share becomes a safe tombstone or is removed according to deletion policy;
- stale cached official content must not remain member-visible.

---

# 5. Tagged people lifecycle edge cases

## Member becomes inactive / leaves Kalam

Historical official publications are preserved.

Behavior:
- publication relationship remains;
- no new notifications are sent to inactive member;
- profile access becomes inactive according to membership policy;
- recognition/history may remain visible to eligible members where policy permits;
- private People fields remain protected.

Do not delete historical recognition because access ended.

## Person identity not yet reconciled

Migration/automation may retain:
- `kalam_app_id`;
- source Webflow member ID;
- unresolved status.

Do not guess canonical `person_id`.

Once verified, link the relationship without duplicating the publication.

## Profile photo changes

- live person chips/profile links may use the current verified avatar;
- approved published campaign creative remains immutable historical publication media.

## Source record disappears/degrades

- preserve existing publication relationship;
- flag staff reconciliation issue;
- do not remove historical content automatically.

---

# 6. Category edge cases

Categories are soft-deactivated, not casually deleted.

If inactive:
- existing publications retain relation;
- category disappears from active publishing choices/member navigation;
- archive may still display it;
- publications remain valid.

Rename:
- preserve category ID;
- update display name;
- slug changes require redirect/alias handling.

---

# 7. Media dependency edge cases

## Approved copied media exists in Connect storage
Use Connect-controlled asset. Loss of original provider/Webflow URL does not break published content.

## Source media unavailable before migration/copy
- preserve source metadata;
- mark missing;
- use an approved fallback only if one exists;
- surface staff exception;
- do not fabricate replacement media.

## Media removed for privacy/security
- remove from member rendering;
- invalidate cached/signed references where possible;
- update affected placements/shares;
- preserve only non-sensitive audit metadata.

## Missing alt text
- block final publication only for media roles where accessibility policy requires alt text;
- staff can add alt text in Media Library/review.

---

# 8. Community dependency edge cases

For Community Feature content:

### Community becomes private
- re-evaluate publication audience;
- all-member placement cannot expose private-community content.

### Community archived
- publication may remain historical if independently valid;
- community CTA becomes inactive/archive state.

### Community removed for policy
- remove/redact community-specific preview/action;
- surface reconciliation warning.

---

# 9. Publication action edge cases

Examples:
- Apply;
- Register;
- Survey;
- Download.

When deadline/end state passes:
- publication may remain readable;
- action becomes disabled/expired;
- card/detail shows closed/ended state.

Broken optional action:
- surface staff exception;
- do not automatically withdraw the whole publication.

Unsafe/invalid URL:
- disable action pending review.

---

# 10. Official-content reporting

Members may report official publications.

Reasons:
- incorrect information;
- inappropriate content;
- privacy concern;
- broken/unsafe link;
- accessibility issue;
- other.

Report volume alone does not automatically hide official content.

Workflow:

```text
member report
→ moderation/publishing queue
→ triage
→ no action / correct / archive / withdraw
→ reason recorded
→ reporter resolution status where appropriate
```

Privacy/security reports receive higher priority.

---

# 11. Moderation authority

### Publisher
- correct normal errors;
- archive;
- reschedule placements.

### Moderator
- triage reports;
- recommend restriction/withdrawal;
- moderate member-created discussion/share content.

### Publishing Manager
- approve material correction;
- withdraw official publication;
- restore/re-publish after correction where valid.

### Platform Admin / Super Admin
- exceptional hard delete;
- emergency restriction;
- access/system intervention.

All privileged actions are audited.

---

# 12. Reaction analytics

UI counts represent current active state.

For a publication:
- reaction_count = members with an active reaction;
- breakdown = current active reaction by type.

Changing Love → Celebrate does not create two current reactions.

Analytics may separately retain event history:
- reaction_set;
- reaction_changed;
- reaction_removed.

---

# 13. Share analytics

UI:
- active_share_count = currently visible/non-withdrawn Timeline Shares that the viewer is authorized to know exist.

Analytics:
- share_created_total;
- unique_sharers;
- active shares;
- removed/hidden shares.

Do not expose private/restricted share counts to unauthorized audiences.

---

# 14. Magazine analytics events

Record:
- event name;
- actor/profile ID where permitted;
- publication/module/placement reference;
- timestamp;
- coarse device/surface metadata;
- campaign/source reference where applicable.

Do not store publication body or private message content inside analytics events.

Initial events:

## Discovery
- `magazine_home_view`
- `magazine_module_impression`
- `publication_card_impression`
- `publication_open`
- `category_open`
- `magazine_filter_apply`
- `magazine_search`
- `search_result_open`

## Engagement
- `publication_reaction_set`
- `publication_reaction_change`
- `publication_reaction_remove`
- `publication_share_start`
- `publication_share_create`
- `publication_action_click`
- `publication_media_play`

Editorial actions belong in staff audit, not ordinary engagement analytics.

---

# 15. Impression and reach definitions

## Card impression
Count when a publication card becomes meaningfully visible in the viewport.

The exact engineering threshold is finalized during implementation but must be consistent across clients.

## Publication open
Count when member opens publication detail.

## Reach
Derived from distinct eligible member viewers for the event/window.

Do not equate raw API request count with reach.

---

# 16. Control Center Magazine metrics

## Publication
- impressions;
- unique reach;
- detail opens;
- reaction count/rate;
- shares;
- unique sharers;
- action clicks;
- media plays where relevant.

## Module
- module impressions;
- publication card impressions;
- opens/click-through;
- reaction/share outcomes;
- current configuration/version.

## Magazine Home
- active members who viewed Home;
- module reach;
- category/filter usage;
- search usage.

## Campaign
Where campaign_ref exists:
- publication reach;
- engagement;
- Connect delivery status;
- related cross-channel receipt references.

Analytics never changes editorial order unless staff explicitly configures engagement sorting.

---

# 17. Analytics privacy boundary

Default staff analytics are aggregate.

Do not provide a general "who viewed this publication" employee-surveillance list.

Individual identity is exposed only where the social feature itself requires it, such as:
- visible reaction participants if later enabled;
- share author;
- comment author on Timeline Share.

Department/team breakdowns should use privacy thresholds where small cohorts could identify individuals.

Private message content is outside Magazine analytics.

---

# 18. Search and archive

## Published
Searchable if viewer is in audience.

## Archived
Searchable/archive-visible if viewer is in audience.

Archive filters may include:
- year/month;
- category;
- publication type;
- person;
- topic/tag.

## Draft/Review/Scheduled
Not in member search.

## Withdrawn
Excluded from normal search/archive.

Old direct link:
- safe unavailable/withdrawn state;
- no stale content leak.

Search authorization must use current audience rules rather than trusting stale index data.

---

# 19. Expiry semantics

Keep separate:

### Placement end
Stops showing in a specific Magazine module.

### Action/deadline expiry
Disables time-sensitive CTA.

### Publication archive
Moves the publication into historical state.

A Hero placement or CTA deadline ending does not destroy the publication.

---

# 20. Analytics vs audit

Product analytics answers:
- reach;
- engagement;
- discovery;
- performance.

Application audit answers:
- who published;
- who withdrew;
- who changed roles/access;
- which layout version shipped;
- how moderation was resolved.

Infrastructure/auth logs can support troubleshooting/security but do not replace Connect's application-level audit trail.

---

# 21. Failure/degraded behavior

## Analytics unavailable
- member publishing/reading continues;
- do not block reactions/shares;
- retry/log where safe.

## Search unavailable
- database/publication access remains authoritative;
- show degraded search rather than unauthorized/incorrect results.

## People lookup unavailable
- existing safe cached/projected identity may render;
- do not provision new identity or guess unresolved people.

## Automation unavailable
- manual publishing remains available.

---

# 22. PDISC-1C exit result

Locked:

- archive vs withdrawal vs delete;
- revision and edit behavior;
- Timeline Share behavior after source changes;
- inactive/unresolved person behavior;
- category/media/community/action dependency handling;
- official-content reporting/moderation;
- current-state reaction/share counts;
- Magazine analytics events and metrics;
- aggregate analytics privacy boundary;
- search/archive rules;
- placement/action/archive separation;
- degraded-state behavior.

With PDISC-1A, PDISC-1B and PDISC-1C locked, **PDISC-1 Magazine Editorial System is COMPLETE**.

Next:
**PDISC-2 — Timeline / Social Graph.**
