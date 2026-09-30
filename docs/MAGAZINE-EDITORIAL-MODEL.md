# Kalam Connect — Magazine Editorial Model

**Status:** PDISC-1A LOCKED  
**Decision record:** `docs/decisions/PDISC-1A-MAGAZINE-HOME-BUILDER-LOCK.md`

## Product definition

Magazine is the **editorially controlled Home of Kalam Connect**.

It is not an algorithmic social feed.

Authorized Kalam staff have 100% control over:

- what appears;
- where it appears;
- when it appears;
- how long it appears;
- visual treatment;
- audience;
- ordering;
- sorting;
- filtering;
- section/module composition.

Automation may create/update content drafts and campaign-linked publication packages. It may not silently change Magazine layout or editorial ordering.

---

# 1. Magazine architecture

Magazine Home is composed from configurable **modules**.

The initial editable starter composition is:

1. Hero Feature
2. Featured / Spotlight
3. Latest from Kalam
4. People & Recognition
5. Events & Opportunities
6. Community Highlights
7. Explore by Category

This is a starter layout, not a hard-coded permanent homepage.

Staff may:
- reorder modules;
- hide/show modules;
- rename configurable module titles;
- add Custom Collection modules;
- change layout presets;
- change sourcing/filter rules;
- schedule module visibility.

---

# 2. Module types

## Hero Feature

Purpose:
- one primary editorial story/campaign.

Rules:
- maximum 1 active primary item;
- manual or explicitly selected content only;
- no engagement-based automatic replacement;
- optional secondary CTA;
- placement schedule independent from publication lifetime.

## Featured / Spotlight

Purpose:
- 2–4 editorially important publications.

Modes:
- manual;
- hybrid.

Use cases:
- major announcements;
- feature stories;
- company news;
- campaigns;
- important events.

## Latest from Kalam

Purpose:
- fresh official publications.

Modes:
- rule-based;
- hybrid.

Typical default:
- published=true;
- member is in audience;
- newest first;
- pinned items first.

## People & Recognition

Purpose:
- people-centric stories.

May include:
- recognition;
- Top Performers;
- birthdays;
- anniversaries;
- welcome/onboarding;
- employee features.

Supports automatic tagged-person projection.

## Events & Opportunities

Purpose:
- upcoming events;
- vacancies/internal opportunities;
- surveys/polls where applicable.

Typical sort:
- event/deadline date;
- then editorial rank.

## Community Highlights

Purpose:
- staff-selected community activity.

This is editorial curation, not automatic "most engaging" content unless staff explicitly configures such a rule.

## Explore by Category

Purpose:
- navigation/discovery.

Can render:
- category tiles;
- category-specific collections;
- topic groups.

## Custom Collection

Purpose:
- any staff-defined editorial collection.

Examples:
- Ramadan;
- Annual Event;
- Academy;
- Sustainability;
- New Joiners;
- Service Delivery Spotlight.

---

# 3. Module configuration contract

Each module has:

- module ID;
- internal name;
- public title;
- enabled state;
- module type;
- layout preset;
- card variant;
- source mode;
- query/filter definition;
- sort definition;
- max items;
- pinned items;
- manual order;
- explicit exclusions;
- audience;
- start time;
- end time;
- theme/accent;
- responsive configuration;
- empty-state behavior;
- revision/version metadata.

---

# 4. Source modes

Each module is exactly one of:

## Manual

Staff selects every item and controls order.

## Rule-based

The system resolves content from a staff-defined rule.

Example:

```text
published = true
category = recognition
audience includes current member
sort = publish_date desc
limit = 6
```

## Hybrid

Rule-based result plus staff overrides.

Supports:
- pinned publications;
- explicit exclusions;
- manual item order;
- automatic fill for remaining slots.

Hybrid is the preferred mode for sections such as Latest and People & Recognition.

---

# 5. Editorial precedence — LOCKED

When resolving a module, apply this order:

1. authorization/audience eligibility;
2. explicit staff exclusion/visibility;
3. manual pinned items;
4. manual item order;
5. module filters/query;
6. module sort rule;
7. publication date as final tie-breaker.

No hidden engagement/recommendation algorithm may override editor intent.

---

# 6. Sorting

Staff-selectable sorting:

- manual;
- publish date newest;
- publish date oldest;
- updated date;
- event date;
- deadline date;
- editorial rank;
- engagement;
- deterministic rotation/random where intentionally configured.

Engagement sorting is opt-in per module.

The default Magazine does not automatically become engagement-ranked.

---

# 7. Filters

Available editorial filters may include:

- publication type;
- category;
- tag/topic;
- related person;
- department/team;
- community;
- campaign;
- date range;
- event state;
- audience;
- featured/pinned state.

Member-facing filters are separately configurable.

Potential member filters:
- category;
- publication type;
- date;
- people;
- department;
- community;
- tag/topic.

Member filtering changes the view; it does not change the canonical editorial layout configuration.

---

# 8. Publication card system

Magazine is card-based, but not every card is identical.

Locked initial card variants:

- Hero;
- Feature;
- Standard;
- Compact;
- Person / Recognition;
- Event;
- Opportunity;
- Announcement;
- Poll.

A card may render:

- category;
- title;
- summary;
- image/video;
- tagged people;
- date;
- reaction summary;
- share count;
- CTA;
- editorial badge;
- event/deadline metadata where relevant.

The Design discovery phase defines final visual treatment and responsive details.

---

# 9. Reactions — LOCKED

Initial reaction set:

- Like;
- Love;
- Celebrate;
- Support;
- Wow;
- Angry.

Rules:

- reactions attach to the canonical Magazine publication;
- one active reaction per member per publication;
- member can change reaction;
- member can remove reaction;
- aggregate reaction counts may be shown;
- member list/details visibility is a later UI/privacy decision;
- staff can disable reactions per publication or publication type;
- reaction notifications should avoid noisy one-notification-per-reaction behavior for high-volume official posts.

---

# 10. Share → Timeline — LOCKED

**Share creates a Timeline Share object.**

```text
Magazine Publication
      ↓ Share
Timeline Share
      ├─ reference to original publication
      ├─ share author
      ├─ optional member commentary
      ├─ audience
      ├─ its own reactions
      ├─ its own comments
      └─ its own replies
```

The original publication remains canonical.

The full publication body is not duplicated into the share record.

The share renders a rich reference/card to the original publication.

---

# 11. Magazine comments — LOCKED

Magazine itself does **not** have one global public comment thread.

Discussion happens on the member's Timeline Share.

Example:

```text
Official Magazine Publication
        ↓
Ahmed shares it
        ↓
Ahmed's Timeline Share
        ├─ reactions
        ├─ comments
        └─ replies

Sara shares the same publication
        ↓
Sara's Timeline Share
        ├─ different reactions
        ├─ different comments
        └─ different replies
```

Magazine may display:
- publication reaction counts;
- share count;
- optional "shared by..." or discussion discovery UI if approved later.

It must not merge all share comments into one Magazine thread.

---

# 12. Tagged people — LOCKED

Official publications can reference one or many people.

Example:

```text
Top Performers
→ Person A
→ Person B
→ Person C
```

For official/staff content, each tagged/related person automatically receives:

1. visible identity reference on the publication;
2. relevance in their personalized Timeline;
3. a profile Tagged projection;
4. a profile Timeline projection when allowed by the final profile display policy;
5. a Recognitions projection when relationship type is recognition-related;
6. a notification unless notification policy suppresses it.

"Public profile" means visible to eligible authenticated Kalam Connect members, not the public internet.

---

# 13. Placement

One canonical publication can be projected to:

- Magazine Home;
- one or more Magazine modules;
- Community Timeline as an official post;
- tagged member profile surfaces;
- a Community page;
- Events;
- Opportunities.

Placement is metadata/projection.

Do not create duplicate publication records merely to show the same publication in multiple places.

---

# 14. Scheduling

Publication timing:

- publish_at;
- expire_at;
- archive_at.

Module timing:

- module_start;
- module_end.

Placement timing:

- placement_start;
- placement_end.

This allows, for example:

```text
Publication remains available for 1 year
Hero placement ends after 5 days
Featured placement ends after 14 days
Archive retains the publication afterward
```

---

# 15. Magazine layout versioning

Magazine Home configuration is versioned.

Required states:

- Draft layout;
- Published layout;
- Historical layout version.

Staff can:

- edit a draft without affecting live Home;
- preview draft;
- publish draft as new live version;
- view previous versions;
- rollback to a prior valid version.

Every publish/rollback action is audited.

---

# 16. Empty-state behavior

Each module must define what happens when fewer items are available than expected.

Options:

- collapse module;
- show fewer items;
- show configured fallback collection;
- preserve layout with placeholder only in preview, never as fake production content.

No module should surface unauthorized or stale content merely to fill a visual slot.

---

# 17. Audience behavior

Magazine respects publication audience first.

A module cannot make a publication visible to a member who is outside the publication's authorized audience.

Audience options may include:

- all eligible members;
- department/team;
- community;
- selected members;
- future approved custom segments.

Preview must support audience simulation for authorized staff.

---

# 18. Editorial archive

Magazine requires:

- publication archive;
- search;
- category navigation;
- people filters;
- tag/topic filters;
- year/month where useful.

Archived content remains linkable unless removed by policy.

---

# 19. Magazine Builder — LOCKED

The Control Center includes a visual **Magazine Builder**.

Staff capabilities:

- create module;
- remove module;
- enable/disable module;
- rename module;
- drag/reorder modules;
- select module type;
- select layout preset;
- select card variant;
- choose Manual / Rule / Hybrid;
- add filters;
- select sorting;
- pin publications;
- exclude publications;
- manually order publications;
- set maximum items;
- select audience;
- set start/end;
- select approved theme/accent;
- configure responsive preset;
- preview desktop/tablet/mobile;
- preview audience;
- save layout draft;
- publish layout version;
- rollback version.

The builder uses approved KDS components/templates.

Ordinary staff do not edit raw CSS.

---

# 20. Automation boundary

Automation may:

- create a publication draft;
- update an automation-owned draft before human release;
- attach campaign/content package references;
- attach approved assets;
- suggest placement metadata where contract allows.

Automation may not:

- silently reorder Magazine modules;
- silently replace the Hero;
- silently alter manual pins;
- silently publish a new Magazine layout;
- bypass publication approval/release rules.

Humans retain final editorial layout authority.

---

# 21. PDISC-1A exit result

The following are now locked:

- 100% staff editorial control;
- module-based Home;
- editable starter layout;
- Manual / Rule / Hybrid source modes;
- editorial precedence;
- card family;
- reaction set;
- Magazine Share → Timeline behavior;
- comments living on Timeline Share;
- official tagged-person projection;
- scheduling/placement separation;
- versioned Magazine layout;
- visual Magazine Builder requirement.

Remaining Magazine work moves to:
- PDISC-1B — publication type/field matrix;
- PDISC-1C — detailed analytics/moderation edge cases;
- PDISC-5 — visual prototypes/design acceptance.
