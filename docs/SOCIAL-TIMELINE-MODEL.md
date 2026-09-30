# Kalam Connect — Social Timeline Model

## Definition

Timeline is the social layer where members:
- publish;
- share;
- react;
- comment;
- reply;
- tag people;
- interact with communities;
- discover activity relevant to them.

Timeline is not the Magazine and not private chat.

---

# 1. Timeline object types

A timeline entry can be:

### Member Post
Original post authored by a member.

### Magazine Share
Member share referencing a Magazine publication.

### Official Projection
A staff publication intentionally placed in Community/Timeline.

### Tagged Projection
A post/publication surfaced because the member is tagged/related.

### Community Post
A post created inside a Community and visible according to membership.

The UI can render these through common PostCard primitives while preserving type/source.

---

# 2. Member post composer

Possible content:
- text;
- image/gallery;
- video;
- document where allowed;
- link;
- poll;
- tagged people;
- selected community;
- optional audience.

Composer must make audience obvious before publishing.

---

# 3. Reactions

Timeline posts/shares support the shared reaction system.

Reaction object should record:
- actor;
- target type/id;
- reaction;
- created/updated time.

A Magazine publication reaction and a Timeline Share reaction are separate contexts.

---

# 4. Comments and replies

Timeline entries host discussion.

Support:
- comment;
- reply;
- edit own;
- delete own where policy permits;
- mention;
- report;
- moderation removal.

Comment visibility follows the parent timeline entry.

---

# 5. Sharing a Magazine publication

```text
Magazine publication
→ Share
→ optional member caption
→ Timeline Share
→ reactions/comments belong to Timeline Share
```

The share card contains a rich reference to the original Magazine publication.

If the original publication is later archived, the share should retain a safe historical reference/preview unless content is removed for policy/security reasons.

---

# 6. Tagging people

## Official/staff content

Tagged people are automatically projected to:
- their personalized Timeline;
- their internal public profile Timeline/Tagged view;
- relevant recognition/profile area.

## Member posts

Member can tag eligible members.

Baseline behavior:
- tagged member is notified;
- post becomes relevant in tagged member's Timeline;
- post appears in tagged member's Tagged profile view;
- default can display it on their profile Timeline automatically;
- tagged member can hide the projection from their own profile or remove their tag subject to policy;
- removing profile projection does not delete the author's post.

This preserves automatic tagging while giving the tagged member basic control against misuse.

---

# 7. Profile timelines

Each member profile can expose separate tabs:

- Timeline — combined public member activity;
- Posts — authored posts;
- Tagged — posts/publications tagging them;
- Media;
- Recognitions;
- Communities;
- About.

Timeline may include:
- own posts;
- own Magazine shares;
- tagged official publications;
- tagged member posts;
- selected community activity according to privacy/product rules.

---

# 8. Feed construction

Start deterministic and understandable.

Candidate tabs:
- For You;
- Following, if follow model is adopted;
- Latest;
- Communities.

MVP can begin with:
- relevance signals from tags/community membership;
- followed people if enabled;
- official Timeline placement;
- recency.

Do not launch with opaque engagement optimization.

---

# 9. Social graph decision

Discovery must decide between:

### Follow model
One-way follow, Instagram-like.

### Connection model
Two-way colleague relationship.

### No explicit graph initially
Feed based on company/community/tag activity.

Do not implement all three.

Recommendation for prototype:
test **Follow** because it is familiar and lightweight, but retain automatic company/community relevance so users do not need to manually follow everyone.

---

# 10. Share/repost types

Potential:
- Share Magazine to Timeline;
- Repost member post;
- Quote/share with commentary.

Discovery must decide whether reposting member posts is needed in MVP.

Magazine Share is definitely required.

---

# 11. Visibility

Possible timeline audiences:
- all eligible members;
- selected community;
- selected people/private small audience only if product needs it later.

Do not turn Timeline into a replacement for Messages.

Private 1:1/group conversation belongs in Messages.

---

# 12. Editing/deletion

Need explicit behavior:
- edit window or unlimited own edit;
- edited indicator;
- deletion semantics;
- how shares behave if source deleted;
- tagged projection cleanup;
- notification cleanup;
- audit requirements for staff/official content.

These must be frozen before schema implementation.

---

# 13. Moderation

Member can:
- report;
- block;
- mute;
- hide own tagged projection.

Moderator can:
- hide/remove content;
- restrict member;
- resolve report;
- preserve audit reason.

Blocking/muting affects feed/profile/message discovery according to final policy.

---

# 14. Analytics

Measure:
- impressions;
- unique viewers;
- reactions;
- comments;
- shares;
- post creation;
- active authors;
- profile visits;
- community interaction.

Do not build engagement mechanics that encourage unhealthy/compulsive behavior simply to increase counts.
