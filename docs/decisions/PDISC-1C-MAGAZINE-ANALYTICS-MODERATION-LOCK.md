# PDISC-1C Decision Lock — Magazine Analytics, Moderation & Edge Cases

**Decision date:** 30/09/2026  
**Status:** LOCKED  
**Authority:** Kalam Connect product owner

## Locked decisions

### Lifecycle
- Archive = normal historical state.
- Withdrawn = exceptional removal for accuracy/privacy/security/policy.
- Hard deletion = rare and privileged.
- Published official content is revisioned.

### Shares
- Timeline Shares reference the canonical publication.
- Source edits update the share preview to the current approved revision.
- Archived source remains shareable/interactive by default.
- Withdrawn source leaves normal feed circulation and locks related share discussion.
- Hard-deleted source cannot remain visible through stale cached share content.

### People
- Historical recognition remains when a member becomes inactive/leaves.
- Unresolved identities are preserved and never guessed.
- Profile-photo changes do not rewrite approved historical campaign creative.

### Dependencies
- categories soft-deactivate;
- copied approved media survives provider/Webflow loss;
- private/removed media is redacted everywhere;
- Community privacy changes re-evaluate publication exposure;
- expired CTAs disable independently from publication history.

### Moderation
- Members can report official content.
- Report count alone never automatically hides official publications.
- Publisher/Moderator/Publishing Manager/Platform Admin have distinct escalation authority.
- Every privileged action is audited.

### Analytics
- UI reaction/share counts represent current active state.
- Analytics may preserve event history separately.
- Reach is based on distinct viewers, not raw API requests.
- Staff view/impression analytics are aggregate by default.
- Do not create a general employee viewer-surveillance list.
- Analytics never silently controls Magazine ranking.
- Product analytics and application audit are separate systems.

### Search/archive
- archived content remains searchable to authorized members;
- withdrawn content is excluded;
- authorization uses current audience, not stale search-index assumptions.

### Reliability
- analytics/search/automation degradation must not take Magazine offline;
- existing safe People projections may render during People outages;
- new identity provisioning cannot guess when People authority is unavailable.

Canonical:
`docs/MAGAZINE-ANALYTICS-MODERATION-EDGE-CASES.md`

Do not reopen during implementation without an explicit product decision.
