# Kalam Connect — Magazine Editorial Model

## Product definition

Magazine is the **editorially controlled home of Kalam Connect**.

It is not an algorithmic social feed.

Authorized Kalam staff control:
- what appears;
- where it appears;
- when it appears;
- how long it appears;
- visual treatment;
- audience;
- ordering;
- sorting;
- filters;
- section composition.

Automation may create drafts/content packages, but it cannot take editorial control away from staff.

---

# 1. Magazine page builder

Magazine Home should be composed from configurable **modules/sections**.

Examples:
- Hero Feature;
- Featured Grid;
- Latest;
- Recognition;
- Birthdays;
- Anniversaries;
- Top Performers;
- Events;
- Opportunities;
- Announcements;
- Community Picks;
- Category Collection;
- Custom Collection.

Each module has:
- ID;
- title;
- visibility;
- layout;
- card style;
- data source;
- sort rule;
- filters;
- maximum items;
- manual pins;
- manual order;
- audience;
- start time;
- end time;
- theme/accent;
- responsive behavior.

## Editorial precedence

A module may be:

### Manual
Every item is selected and ordered by staff.

### Rule-based
Staff defines a query such as:
`category=recognition AND published=true ORDER BY published_at DESC LIMIT 6`.

### Hybrid
Rule-based collection with manually pinned items and explicit order overrides.

**Manual/pinned placement always wins.**

No algorithm may silently rearrange editor-controlled modules.

---

# 2. Publication cards

Magazine content is shown primarily as cards.

Card variants can include:
- Hero;
- Feature;
- Standard;
- Compact;
- Person/Recognition;
- Event;
- Opportunity;
- Announcement;
- Poll.

Cards may contain:
- category;
- title;
- summary;
- image/video;
- tagged people;
- date;
- reaction counts;
- share count;
- CTA;
- editorial badge such as Featured/Pinned.

---

# 3. Magazine reactions

Magazine cards support reactions directly on the canonical publication.

Reaction set should be configurable before implementation.

Candidate set:
- Like;
- Love;
- Celebrate;
- Support;
- Wow;
- Angry.

The exact iconography/labels belong to design discovery.

Rules:
- one active reaction per member per publication;
- member can change/remove reaction;
- aggregate counts shown according to UI rules;
- reaction activity may generate notifications only where meaningful;
- staff can disable reactions per publication/type if needed.

---

# 4. Magazine share model

**Share creates a Timeline object.**

```text
Magazine Publication
      ↓ Share
Timeline Share Post
      ├─ reference to original publication
      ├─ member caption/commentary (optional)
      ├─ share author
      ├─ share audience
      ├─ its own comments
      └─ its own social interactions
```

The original publication remains one canonical object.

Do not duplicate the full article/body into each share.

---

# 5. Comment model

The Magazine itself does **not** need one giant global public comment thread.

Discussion is attached to the member's **Timeline Share Post**.

This matches the intended behavior:

- a member sees a Magazine card;
- reacts to it directly if desired;
- shares it to their Timeline;
- may add commentary;
- other members comment on that share;
- those comments belong to that share context.

Magazine may display:
- reaction counts;
- share count;
- optional links to active discussions/shares.

It should not merge all share comments into one uncontrolled Magazine thread.

This rule needs owner confirmation during prototype testing, but it is the planning baseline.

---

# 6. Tagged people

Official publications can reference one or many people.

Example:
```text
Top Performers
→ Person A
→ Person B
→ Person C
```

When a person is tagged/related:

1. publication shows their identity card/tag;
2. it becomes relevant in that person's personalized Timeline;
3. it appears on that member's internal public profile Timeline/Tagged view;
4. recognition may appear in a dedicated Recognitions tab;
5. the person receives a notification unless disabled by policy.

For official/staff publications, this projection is automatic.

For member-created posts, tagged-member behavior is defined in the Social Timeline model.

"Public profile timeline" means visible to eligible authenticated Kalam Connect members, not the public internet.

---

# 7. Placement

A publication may be placed in:

- Magazine Home;
- one or more Magazine modules;
- Community Timeline as an official post;
- tagged member profile timelines;
- community page;
- event/opportunity surfaces.

Placement is metadata/projection, not duplicate content.

---

# 8. Sorting

Staff-configurable module sort options may include:
- manual order;
- publish date;
- updated date;
- event date;
- engagement;
- random/rotation where intentionally configured;
- custom rank.

Default Magazine Home does not automatically become engagement-ranked.

---

# 9. Filters

Staff controls which filters exist and where.

Potential member filters:
- category;
- publication type;
- date;
- people;
- department;
- community;
- tags.

Filtering changes the member view but does not change the canonical editorial layout configuration.

---

# 10. Scheduling

Publication:
- publish_at;
- expire_at;
- archive_at.

Module placement:
- placement_start;
- placement_end.

This allows:
- publication stays available in archive/profile;
- hero placement expires;
- another story replaces it;
- staff does not need to manually remove every placement.

---

# 11. Editorial archive

Magazine requires:
- published archive;
- search;
- categories;
- people/tag filters;
- year/month filters where useful.

Archived content remains linkable unless policy removes it.

---

# 12. Control Center requirements

Magazine Studio must support:
- visual module ordering;
- drag/reorder;
- manual item selection;
- rule-builder;
- filters;
- preview;
- device preview;
- audience preview;
- schedule;
- publish;
- rollback/revision;
- audit history.

Automation-generated content enters as draft/review material.

Humans retain final editorial layout authority.
