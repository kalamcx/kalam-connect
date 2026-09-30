# Kalam Connect — Social Timeline / Social Graph Model

**Decision date:** 30/09/2026  
**Status:** PDISC-2 LOCKED  
**Scope:** Member posts, Magazine shares, tagging, follows, feeds, reactions, comments/replies, reposts, visibility, moderation and social analytics.

## Product definition

Timeline is Kalam Connect's **member-driven social layer**.

Members use it to:
- publish;
- share Magazine content;
- follow colleagues;
- tag and mention people;
- react;
- comment/reply;
- repost/quote;
- interact with Communities;
- discover relevant member activity.

Timeline is not:
- the editor-controlled Magazine;
- private direct/group messaging;
- a replacement for company employee records.

All Timeline content remains inside the authenticated Kalam Connect membership boundary unless a future explicit product decision adds an external-sharing surface.

---

# 1. Canonical social objects

Do not store every feed appearance as a duplicate post.

The feed renders projections of canonical objects.

## A. Member Post

Original member-authored social post.

Supports:
- text;
- image/gallery;
- video;
- safe link preview;
- attachment/document where policy allows;
- structured people tags;
- text mentions;
- Community scope where applicable.

Member polls are **not required for the initial Timeline MVP**. Official Poll publications remain supported. Member/community polls may be added later by explicit decision.

## B. Magazine Share

A member-authored Timeline post referencing one canonical Magazine publication.

Contains:
- source publication ID;
- member commentary/caption, optional;
- author;
- audience/scope;
- its own reactions;
- its own comments/replies.

The official publication body is referenced, not copied.

## C. Quote Post

A member-authored post referencing another member post with new commentary.

Contains:
- source post ID;
- new commentary;
- author;
- audience/scope;
- its own reactions;
- its own comments/replies.

## D. Repost

Distribution action on another member post.

A Repost:
- has no caption;
- does not create a second discussion thread;
- does not create separate reactions;
- attributes the original author;
- can be undone by the reposter;
- increases distribution of the original post.

Reactions/comments remain attached to the original post.

## E. Official Timeline Projection

An approved Magazine publication intentionally placed into Timeline.

It remains the canonical Magazine publication.

Interactions:
- reactions attach to the publication;
- member can Share it to create a Magazine Share;
- there is no global direct comment thread on the official publication.

This preserves the locked Magazine discussion model.

## F. Tagged Projection

A feed/profile projection caused by a structured people tag/relationship.

Projection is not a duplicate content record.

## G. Community Post

A Member Post or Quote Post scoped to a Community.

Community is a visibility/scope relationship, not a separate incompatible social content system.

---

# 2. Recommended data model

Planning names:

### `social_posts`
Canonical member-authored post objects.

Important fields:
- id;
- author_profile_id;
- kind: original / magazine_share / quote;
- body;
- source_publication_id nullable;
- source_post_id nullable;
- community_id nullable;
- audience_type;
- comments_enabled;
- edited_at;
- deleted_at;
- moderation_state;
- created_at;
- updated_at.

Do not use a database enum unless implementation has a strong reason; controlled registry/check constraints are preferred.

### `post_media`
- post_id;
- media_asset_id;
- role;
- sort_order;
- alt text/metadata where appropriate.

### `post_people`
Structured member tags.

- post_id;
- profile/person reference;
- relationship_type = tagged;
- created_at;
- hidden_from_tagged_profile_at nullable;
- tag_removed_at nullable.

### `mentions`
Structured references parsed/created from text.

Mentions may target:
- member;
- Community where later supported.

Mention is not the same as Tag.

### `post_reposts`
- source_post_id;
- profile_id;
- created_at.

Unique:
`source_post_id + profile_id`.

### `follows`
- follower_profile_id;
- followed_profile_id;
- created_at.

Unique pair.

### `post_revisions`
Moderator-visible revision history for member content.

### `comments`
Discussion attached to social posts/shares/quotes.

### `comment_reactions`
Initial comment interaction uses simple Like.

### Post reactions
Use the shared Timeline reaction model:
- Like
- Love
- Celebrate
- Support
- Wow
- Angry

Implementation may use a common safe reaction table where RLS remains clear.

---

# 3. Member composer — LOCKED

Initial composer supports:

- text;
- image;
- gallery;
- video;
- safe link;
- approved document/attachment;
- tag people;
- mention people;
- choose eligible Community where posting permission exists.

The composer must always make destination/visibility obvious before Publish.

## Default destination

`All Kalam Members`.

Member may instead choose an eligible Community.

Do not expose "selected private people" as a Timeline audience in MVP.

Small/private conversation belongs in Messages.

## Limits

Use configurable anti-abuse limits.

Initial product baseline:
- maximum 20 structured people tags on a member post;
- maximum 10 text mentions per post/comment;
- official/staff publication workflows can exceed member tag limits when validated by trusted server rules.

Exact media-size/count limits are engineering configuration, not product semantics.

---

# 4. Audience / visibility — LOCKED

Initial member-post audiences:

1. `all_members`
2. `community`

No public-web audience.

No one-to-one/private-small-group Timeline audience.

## Audience cannot be widened through sharing

For Magazine Share, Quote Post or Repost:

```text
effective audience
= source audience ∩ destination audience
```

A share/repost can never expose source content to someone who cannot see the source.

## Post destination is immutable after publish

A published post cannot be moved:
- All Members → another Community;
- Community A → Community B;
- Community → All Members.

Reason:
changing scope after interactions/shares makes privacy and RLS behavior difficult to reason about.

Member may:
- edit allowed content fields;
- delete the post;
- create a new post in another destination.

## Official publication audience

Official publication audience remains authoritative.

Tagging or sharing never widens it.

---

# 5. Tag vs Mention — LOCKED

## Tag

A structured relationship between a post and a member.

Tag causes:
- tagged member notification;
- high relevance in tagged member's personalized Timeline;
- Tagged profile projection;
- default profile Timeline projection;
- optional Media projection if relevant.

## Mention

An inline `@member` reference in text/comment.

Mention causes:
- linked identity;
- notification;
- relevance signal.

Mention does **not** automatically place the content in the person's Tagged profile tab.

This distinction avoids every casual @mention becoming permanent profile content.

---

# 6. Tagged-member control — LOCKED

## Member-authored post

Tagged member may:

### Hide from profile
- leaves tag intact;
- removes the item from their profile Timeline/Tagged presentation where configured;
- author post remains unchanged.

### Remove tag
- removes structured association to the tagged member;
- removes tagged profile projection;
- stops future tag-based notifications/relevance;
- does not delete or edit the author's post.

System may retain safe moderation/audit metadata.

## Official publication

Tagged/recognized member may:
- hide the profile projection where policy permits;
- report/request correction.

They cannot directly rewrite/remove an official recognition relation from the source publication.

Publisher/authorized staff resolves the official relationship.

---

# 7. Profile Timeline projection — LOCKED

An authenticated member's internal-public profile can show:

### Timeline
Combined member activity:
- authored posts;
- Magazine Shares;
- Quote Posts;
- tagged member posts unless hidden/removed;
- tagged official publications;
- recognition projections;
- Community activity only when the viewer can access that Community.

### Posts
Member-authored original posts + quote posts.

### Tagged
Structured member tags + official tagged publications.

### Media
Eligible media from authored/tagged content according to visibility.

### Recognitions
Official recognition/people-milestone projections.

### Communities
Visible membership according to Community/profile privacy rules.

Profile projection never bypasses the source object's audience.

"Public profile" means internal to authenticated eligible Kalam Connect members.

---

# 8. Social graph — FOLLOW model LOCKED

Kalam Connect uses a **one-way Follow model**.

It does not use:
- friend requests;
- mutual connection approval;
- separate "connection" graph.

Why:
- lower friction;
- familiar social behavior;
- better discovery in a 2,000+ member organization;
- avoids requiring two-party approval for routine social discovery.

## Follow rules

- any active eligible member can follow another active eligible member unless blocked/restricted;
- follow does not require approval;
- unfollow is immediate;
- following yourself is invalid;
- duplicate follow is impossible;
- follow relation is removed/prevented by a block;
- inactive members cannot gain new followers or create new follow activity.

## Follow notification

Member receives an in-app follow notification, subject to notification preferences.

High-volume follow events may be aggregated.

## Organizational relevance

Do not auto-create fake Follow relationships from:
- department;
- team;
- manager;
- People data.

The feed may use explicit organization/content relevance without pretending the user chose to follow those people.

---

# 9. Feed tabs — LOCKED

Initial Timeline tabs:

1. **For You**
2. **Following**
3. **Latest**
4. **Communities**

Member may later choose a preferred default in Settings.

## For You

Default discovery feed.

Use understandable deterministic signals, not opaque engagement-maximizing ML.

Priority signals:

1. content explicitly tagging the member;
2. content from followed members;
3. content from joined Communities;
4. approved official Timeline projections;
5. recent eligible network content;
6. diversity/recency controls to avoid one author dominating.

Optional lightweight engagement signals may be introduced later only as transparent secondary signals.

Do **not** rank using:
- private message contents;
- private message relationship intensity;
- HR/performance data;
- salary;
- sensitive People attributes;
- hidden manager assessments.

Where useful, UI can explain:
- Tagged you
- You follow Ahmed
- From Community X
- Official Kalam post

## Following

Reverse-chronological eligible activity from people the member follows.

Includes:
- original posts;
- Magazine Shares;
- Quote Posts;
- Reposts.

Does not silently inject unrelated network content.

Critical official communication belongs in Magazine/notifications rather than being disguised as a followed-person post.

## Latest

Reverse-chronological eligible all-member activity.

Excludes content outside the viewer's Community/audience permissions.

## Communities

Eligible activity from Communities the member has joined/can access.

Community-specific feed behavior is refined in PDISC-Communities.

---

# 10. Feed pagination / consistency

Requirements:

- cursor-based pagination;
- stable ordering within a request window;
- no duplicate cards while paging;
- deleted/withdrawn/permission-lost objects disappear safely;
- source authorization is checked when rendering, not trusted solely from cached ranking data.

Realtime should not constantly reorder a member's current viewport.

New activity can surface through:
- "New posts" indicator;
- user-triggered refresh;
- deliberate top insertion when UX accepts it.

---

# 11. Reactions — LOCKED

Timeline posts, Magazine Shares and Quote Posts use the shared six reactions:

- Like
- Love
- Celebrate
- Support
- Wow
- Angry

Rules:
- one active reaction per member per target;
- member can change/remove;
- current UI count reflects active state;
- reaction event history may be retained for analytics separately.

## Comments/replies

Comments and replies use a lightweight **Like** interaction initially.

Do not open the six-reaction picker on every comment in MVP.

This keeps discussions visually lighter.

---

# 12. Comments / replies — LOCKED

Every Member Post, Magazine Share and Quote Post supports discussion unless `comments_enabled=false`.

Initial structure:
- top-level comment;
- one nested reply level.

A reply to a reply is visually/structurally attached to the same top-level thread.

This avoids deeply nested discussion trees.

## Comment author

May:
- edit own comment;
- delete own comment;
- report other comments;
- mention eligible members.

Edited comments show `Edited`.

## Post author

May:
- turn comments off/on;
- hide a comment from their own post.

"Hiding" is not destructive deletion:
- normal viewers stop seeing the comment;
- comment remains available to moderation/audit;
- commenter is not silently erased from system evidence.

## Moderator

May:
- remove/hide;
- restore where policy allows;
- record reason;
- restrict commenter/member.

## When comments are turned off

Existing comments remain readable by default but become read-only.

The author can re-enable comments.

Moderation can lock comments independently when required.

---

# 13. Repost — LOCKED

Member posts can be Reposted.

Repost:
- references original;
- no new caption;
- no new comment thread;
- no separate reactions;
- increases distribution;
- shows original author and reposter;
- may be undone.

The source post's counts/interactions remain canonical.

## Repost source change

Source edited:
- repost displays current source;
- source shows Edited where applicable.

Source deleted:
- repost disappears from normal feed.

Source removed by moderation:
- repost disappears immediately from normal feed.

Source audience restriction/loss:
- repost disappears for viewers no longer authorized.

---

# 14. Quote Post — LOCKED

Member may quote another eligible member post and add commentary.

Quote:
- is a new `social_post`;
- references original;
- has own reactions;
- has own comments;
- preserves quote author commentary.

## Source edited
Quote preview resolves latest source version and shows source Edited indicator when applicable.

## Source deleted by original author
Quote may remain because the quoting member's commentary is their own content.

Source preview becomes:
`Original post unavailable`.

Do not retain deleted source body/media in the quote.

## Source removed for moderation/privacy/security
- remove source preview;
- temporarily hide/restrict quote from normal feed if necessary;
- moderator determines whether independent quote commentary can remain.

---

# 15. Magazine Share — LOCKED

Magazine Share follows PDISC-1 rules.

Member:
- selects Share;
- optionally writes commentary;
- selects eligible destination;
- publishes.

Magazine Share:
- has own Timeline reactions;
- has own comments/replies;
- references canonical publication;
- cannot widen publication audience.

A member may remove their own Magazine Share without affecting the original Magazine publication.

---

# 16. Member post editing — LOCKED

Member may edit:
- text/body;
- link description where user-authored;
- alt text;
- structured people tags;
- comments_enabled setting.

Member may **not** after publish:
- change destination/audience;
- change post kind;
- switch source publication/post;
- replace/add/remove primary media attachments in MVP.

Reason:
immutable media/destination keeps shares, moderation, caching and privacy predictable.

If member needs different media/destination:
- delete/soft-delete;
- create a new post.

## Edited indicator

Any meaningful post-body/tag change after publish:
- records revision;
- sets `edited_at`;
- shows `Edited` to members.

Moderators can inspect revisions.

Normal members do not receive a full edit-history viewer in MVP.

## Tag edits

Adding a tag:
- creates projection;
- sends notification.

Removing a tag:
- removes projection;
- follows tagged-member rules.

---

# 17. Member post deletion — LOCKED

Normal member delete = **soft delete**.

Effects:
- post leaves Timeline;
- leaves author profile;
- leaves search;
- new interaction disabled;
- structured tagged projections removed;
- Reposts disappear;
- notifications linking only to that post resolve safely.

## Quote Posts referencing deleted source

Quote author's commentary may remain.

Original preview becomes unavailable.

## Comments

Deleted source post discussions are no longer member-visible.

Retention/purge of deleted records is a later company privacy/retention implementation policy.

---

# 18. Comment deletion — LOCKED

Member deletes own comment:

If no replies:
- remove from normal UI.

If replies exist:
- render `Comment removed` tombstone;
- preserve valid replies and thread context.

Moderator removal behaves similarly but records moderator reason.

---

# 19. Blocks — LOCKED

Block is a social safety feature, not a way to erase company identity.

When A blocks B:

- existing follow relations between A/B are removed;
- future follows prevented;
- DMs/new conversations between them prevented;
- structured tags/mentions between them prevented;
- each other's member-generated posts are hidden from global Timeline/profile discovery where practical;
- social notifications between them stop.

Block does **not** hide:
- official Kalam publications;
- required company announcements;
- the existence of the person in authorized People Directory results.

## Shared Community

In a shared Community, blocked-member content is collapsed/limited rather than destroying thread context for everyone.

Community moderation rules remain authoritative.

Exact visual treatment is finalized in prototype/design discovery.

---

# 20. Mute — LOCKED

Mute is private and does not notify the muted member.

Mute:
- removes/mutes that member's member-generated activity from For You/Latest where possible;
- can suppress non-essential social notifications from them;
- does not remove follow automatically;
- does not block profile access;
- does not prevent DM by itself.

Conversation mute is separate from member mute.

---

# 21. Social moderation — LOCKED

Member may report:

- post;
- Magazine Share;
- Quote Post;
- Repost/source relationship;
- comment/reply;
- profile/member.

Initial reasons:
- harassment/bullying;
- inappropriate content;
- spam;
- privacy/confidential information;
- impersonation/misrepresentation;
- unsafe link/file;
- misinformation/incorrect internal information;
- other.

Report count alone does not automatically remove content.

Technical anti-spam/rate-limiting may restrict obvious abusive activity independently.

## Moderator actions

- no action;
- hide content;
- remove content;
- restore;
- lock comments;
- restrict posting;
- restrict commenting;
- escalate member account issue;
- record warning/decision.

## Member Admin / Platform Admin

Account suspension/access changes are separate from content moderation and remain subject to People/access authority.

Every privileged moderation action is audited.

---

# 22. Social notifications — LOCKED

Trusted server actions create notifications for:

- tag;
- mention;
- reaction;
- comment;
- reply;
- follow;
- repost;
- quote;
- Magazine Share interaction;
- moderation outcome where appropriate.

Rules:
- no self-notification;
- high-volume reaction/follow events may aggregate;
- muted/blocked relationships suppress applicable notifications;
- notification never grants access to content the recipient cannot currently view.

---

# 23. Social search — LOCKED

Search may return eligible:
- member posts;
- Magazine Shares;
- Quote Posts;
- people;
- Communities.

Reposts do not need their own search result; the source post is searchable.

Search respects:
- source audience;
- Community access;
- deleted/moderated state;
- block rules where applicable.

---

# 24. Social analytics — LOCKED

## Member-facing own-post metrics

Author may see:
- impressions/reach count;
- reactions;
- comments;
- reposts;
- quote count;
- Magazine Share interaction where applicable.

No general viewer identity list.

## Product/staff aggregate metrics

- daily/weekly/monthly active social members;
- post authors;
- posts created;
- comments/replies;
- reactions;
- reposts/quotes;
- Magazine Shares;
- follow activity;
- Community participation;
- report/moderation volume;
- feed-tab usage;
- feed impressions/open rates.

Do not use analytics to create employee performance scores.

Do not expose "who viewed whose post" as a general workplace surveillance tool.

---

# 25. Social analytics events

Initial:

### Feed
- `timeline_view`
- `timeline_tab_change`
- `timeline_post_impression`
- `timeline_post_open`
- `timeline_refresh`

### Creation
- `post_create`
- `post_edit`
- `post_delete`
- `magazine_share_create`
- `repost_create`
- `repost_remove`
- `quote_create`

### Engagement
- `post_reaction_set`
- `post_reaction_change`
- `post_reaction_remove`
- `comment_create`
- `comment_reply_create`
- `comment_like`
- `follow_create`
- `follow_remove`

### Safety
Moderation/report actions belong primarily in trusted audit/moderation records, not ordinary engagement analytics.

---

# 26. Feed safety / anti-abuse

Support configurable:
- post rate limit;
- comment rate limit;
- tag/mention limits;
- link/file validation;
- upload validation;
- duplicate/spam detection;
- temporary restriction.

Do not use invisible popularity suppression as the primary moderation system.

Member should receive a clear state when a post/action is blocked by policy/rate limits.

---

# 27. Inactive/leaver author

When a member becomes inactive:

- cannot create/edit/react/comment/follow;
- authored historical social posts may remain according to retention policy;
- profile becomes inactive;
- follow graph remains historical or is excluded from active counts according to implementation;
- new DMs/social notifications stop;
- member-generated content is not automatically deleted solely because employment/access ended.

Moderator/retention policy can remove content independently.

---

# 28. Failure / degraded states

## Realtime unavailable
- posting and feed reading continue through standard request/refresh path;
- "new posts" realtime indicator may degrade.

## Feed ranking service unavailable
- fall back to Latest eligible chronological feed.

## Search unavailable
- Timeline/feed remains available.

## People projection unavailable
- existing safe cached profile display may render;
- new tag/follow resolution requiring People authority may fail safely;
- never guess identity.

## Media processing unavailable
- block final media publish or hold upload pending;
- text-only posts can continue if independent.

---

# 29. Design requirements carried into PDISC-5

Timeline design must make these states visually distinct:

- original member post;
- Magazine Share;
- Quote Post;
- Repost;
- Official Timeline Projection;
- Community Post;
- Tagged you;
- Edited;
- comments locked;
- source unavailable;
- blocked/collapsed content;
- deleted comment tombstone.

The product should feel premium and calm, not like a generic admin feed.

---

# 30. PDISC-2 exit result

Locked:

- canonical Timeline object types;
- member composer scope;
- member audiences;
- destination immutability;
- Tag vs Mention semantics;
- tagged-member control;
- automatic profile/timeline projections;
- one-way Follow model;
- For You / Following / Latest / Communities feeds;
- deterministic For You ranking principles;
- six post reactions + simple comment Like;
- one-level comment replies;
- Repost behavior;
- Quote Post behavior;
- Magazine Share behavior;
- post edit/media/destination rules;
- soft deletion/tombstones;
- Block/Mute semantics;
- social moderation;
- notifications;
- search;
- analytics/privacy;
- inactive-member behavior;
- degraded fallbacks.

**PDISC-2 Timeline / Social Graph is COMPLETE / LOCKED.**

Next:
**PDISC-3 — Profiles / Settings / Roles.**
