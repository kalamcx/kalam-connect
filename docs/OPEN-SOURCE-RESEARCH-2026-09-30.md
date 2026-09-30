# Kalam Connect — Open-Source & UX Research

**Date:** 30/09/2026  
**Purpose:** identify patterns and potential reusable code without prematurely selecting a codebase.

## Research rule

A project can be:
- a **behavior reference**;
- a **design reference**;
- an **architecture reference**;
- a **code/component reuse candidate**.

Those are different classifications.

No repository should be forked into Kalam Connect until stack, security, license and maintenance fit are reviewed.

---

# 1. HumHub — enterprise social/community reference

Repository:
`humhub/humhub`

Useful ideas:
- users with configurable profiles;
- Spaces for departments/projects/events;
- content/interaction;
- network-operator permissions;
- notifications;
- modules such as calendar, polls, direct messages and SSO.

Best use:
**product/permission/community reference**.

Caution:
- PHP/Yii stack differs from planned React/Supabase direction;
- dual AGPL/proprietary licensing requires legal/license awareness for direct reuse.

Recommendation:
study, do not adopt as base at this stage.

---

# 2. Discourse — community/moderation/chat reference

Repository:
`discourse/discourse`

Useful ideas:
- mature discussions;
- realtime chat;
- groups;
- moderation;
- themes/plugins;
- accessibility practices;
- admin/community operations.

Best use:
**moderation, discussion, admin and community-governance reference**.

Caution:
- large Rails application;
- GPLv2;
- forum-first information architecture differs from Kalam Connect.

Recommendation:
reference behavior, not base product.

---

# 3. Mastodon — feed/safety/moderation reference

Repository:
`mastodon/mastodon`

Useful ideas:
- chronological/realtime timelines;
- media;
- profile/follow graph;
- privacy;
- blocking/muting;
- reporting/moderation.

Best use:
**feed, moderation and social safety reference**.

Caution:
- federation/ActivityPub complexity not needed;
- Rails/Redis/Sidekiq stack;
- AGPLv3.

Recommendation:
reference only unless a specific isolated pattern is deliberately reimplemented.

---

# 4. Bluesky social-app — modern social UX reference

Repository:
`bluesky-social/social-app`

Useful ideas:
- modern feed/profile/composer navigation;
- multiple feed concepts;
- moderation layers;
- mobile-first interaction;
- production-scale social client patterns.

License:
MIT.

Best use:
**high-value interaction/design/code-pattern research**.

Caution:
- AT Protocol architecture is not Kalam Connect's backend;
- React Native/web architecture should not be imported blindly.

Recommendation:
one of the strongest references for modern social UX.

---

# 5. Zulip — messaging/threading reference

Repository:
`zulip/zulip`

Useful ideas:
- async + realtime conversation;
- clear unread state;
- topic-based threading;
- mature team-chat behavior.

License:
Apache 2.0.

Best use:
**messaging interaction/notification/threading reference**.

Caution:
- product is conversation-first rather than social/magazine-first.

Recommendation:
study messaging behavior; do not adopt whole app.

---

# 6. Rocket.Chat — room/channel/messaging reference

Repository:
`RocketChat/Rocket.Chat`

Useful ideas:
- direct messages;
- groups/channels;
- file sharing;
- reactions;
- mentions;
- search;
- realtime presence.

Best use:
**messaging/community-room reference**.

Caution:
- large open-core product;
- licensing/edition boundaries must be reviewed before code reuse;
- far more communication features than Kalam Connect MVP needs.

Recommendation:
reference only until license/stack decision.

---

# 7. Clonagram — Next.js + Supabase social UI candidate

Repository:
`zivavu/Clonagram`

Current project claims:
- Next.js;
- Supabase Auth/Postgres/Storage/Realtime;
- Google OAuth + email;
- responsive UI;
- light/dark;
- feed;
- profiles;
- explore;
- stories/reels;
- direct messages.

License:
MIT.

Strength:
very close to the proposed Kalam technical direction.

Risk:
- young/small project;
- low adoption compared with mature platforms;
- clone behavior is not evidence of production hardening.

Recommendation:
**audit as potential UI/component/prototype donor, not architecture authority**.

---

# 8. ciaorelated — Instagram-style groups/events/chat candidate

Repository:
`dogankaraarslan1/ciaorelated`

Useful ideas:
- feed;
- profiles;
- media posts;
- tagged users;
- group/community links;
- events;
- chat;
- explore/search.

License:
MIT.

Stack:
React Native/Expo + GraphQL/Prisma/Postgres.

Best use:
**mobile interaction and community-flow reference**.

Caution:
not the same web stack and still relatively young.

Recommendation:
study flows/components; selective ideas only.

---

# 9. What we should NOT do

Do not:
- fork Mastodon and remove federation;
- fork Discourse and force it to look like Instagram;
- use HumHub simply because it already says "enterprise social network";
- copy an Instagram clone and assume security/roles/moderation are production-ready;
- add stories/reels because a clone has them;
- accept another project's database model as Kalam truth.

---

# 10. Reuse decision framework

Score every candidate component/project on:

1. UX quality;
2. accessibility;
3. performance;
4. React/TypeScript fit;
5. Supabase fit;
6. security maturity;
7. code quality;
8. test quality;
9. maintenance activity;
10. license compatibility;
11. amount of unwanted architecture;
12. KDS adaptability.

Possible outcomes:
- reference only;
- copy interaction concept;
- adapt isolated component;
- adapt subsystem;
- reject.

---

# 11. Current research conclusion

Do **not** select one open-source platform as Kalam Connect's foundation yet.

Current strongest reference mix:

- **Bluesky** → modern feed/profile/composer/moderation UX;
- **HumHub** → enterprise member/Space/permission concepts;
- **Discourse** → moderation/admin/community operations;
- **Zulip/Rocket.Chat** → messaging;
- **Mastodon** → safety/feed mechanics;
- **Clonagram** → Next.js + Supabase implementation experiments;
- **ciaorelated** → modern mobile groups/events/social patterns.

The next step is to convert research into a Kalam-specific function and interaction map, then prototype the product before deciding what code is reusable.
