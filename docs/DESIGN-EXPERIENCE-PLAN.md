# Kalam Connect — Design & Experience Discovery

## Design goal

Kalam Connect should not look like an internal HR portal and should not be an Instagram clone.

The goal is a premium internal social product that combines:
- editorial magazine quality;
- modern social interaction;
- high-quality profiles;
- strong people photography;
- fast messaging;
- clear community identity;
- elegant staff controls.

"Better than Instagram" means:
- clearer information hierarchy;
- stronger editorial storytelling;
- less visual clutter;
- more deliberate interaction;
- better desktop experience;
- better accessibility;
- better connection between company stories and people;
- no dark patterns designed only to maximize scrolling.

---

# 1. Product visual personality

Keywords:
- premium;
- human;
- expressive;
- editorial;
- youthful;
- confident;
- warm;
- clean;
- responsive;
- fast.

Avoid:
- corporate intranet look;
- generic admin dashboard look on member surfaces;
- excessive cards-with-borders everywhere;
- heavy gradients/glass;
- noisy gamification;
- fake AI faces.

---

# 2. Shared design system

Kalam Connect should consume Kalam Design System (KDS).

KDS provides:
- typography;
- semantic color;
- spacing;
- radius;
- border;
- shadow;
- motion;
- breakpoints;
- core controls.

Connect adds product-level patterns:
- magazine cards;
- editorial modules;
- post cards;
- share cards;
- reaction bars;
- profile headers;
- community headers;
- message bubbles;
- composer;
- notification items;
- Control Center editorial builder.

---

# 3. Magazine visual system

Magazine Home should have an editorial rhythm.

Possible composition:
- immersive hero;
- asymmetric feature grid;
- horizontal people/recognition rail;
- latest cards;
- event/opportunity cards;
- category collections.

Not every item should use the same rectangular card.

Card system should support:
- portrait;
- landscape;
- square;
- text-led;
- people-led;
- image-led;
- compact.

Editorial staff choose approved layouts through the Control Center.

---

# 4. Timeline visual system

Timeline should be simpler than Magazine.

Principles:
- author identity first;
- post body readable;
- media dominant only when media exists;
- reactions/comments/share obvious but visually quiet;
- tagged people represented elegantly;
- Magazine Share visually distinguishable from original member post.

Mobile:
- single primary content column.

Desktop:
- centered social column with contextual side panels only where useful;
- avoid huge empty margins and dashboard feeling.

---

# 5. Profile visual system

Profile should feel like a high-quality member identity page.

Header:
- full-width cover;
- avatar overlapping cover;
- name/title/department;
- concise bio;
- Follow/Message actions if adopted.

Profile content should visually separate:
- authored posts;
- tagged content;
- recognitions;
- media;
- communities;
- about.

Recognition should feel celebratory without turning profiles into HR records.

---

# 6. Community visual system

Each Community gets:
- cover/theme;
- name;
- description;
- member count;
- privacy status;
- join state;
- feed;
- members;
- optional chat.

Community identity may use approved accent/category colors without breaking the shared system.

---

# 7. Messaging visual system

Aim for calm, fast and familiar.

Desktop:
- conversation list;
- active conversation;
- optional details panel.

Mobile:
- conversation list → conversation transition.

Features should prioritize:
- message legibility;
- unread state;
- attachment clarity;
- participant identity;
- fast compose.

Do not overload messaging MVP with every Discord/Slack feature.

---

# 8. Control Center visual system

Control Center may use denser application UI than member surfaces.

It must still use KDS.

Core views:
- editorial calendar/list;
- publication editor;
- Magazine layout builder;
- Media Library;
- preview lab;
- moderation queue;
- campaign/delivery monitor;
- analytics;
- settings/roles.

Magazine layout builder should visually represent the actual page modules and support reorder/pin/rule configuration.

---

# 9. Motion

Motion should reinforce:
- navigation;
- reaction feedback;
- share completion;
- modal/sheet transitions;
- media viewing;
- loading.

Avoid:
- constant decorative motion;
- long page transitions;
- animations that delay interaction.

Respect reduced-motion preferences.

---

# 10. Responsive design

Prototype at minimum:
- small mobile;
- large mobile;
- tablet;
- standard desktop;
- wide desktop.

Do not treat mobile as a shrunken desktop.

Magazine layout may change substantially across breakpoints while preserving editorial ordering.

---

# 11. Design prototypes required before implementation

Prototype these flows:

### Flow A — Magazine
Home → article → react → share → Timeline Share.

### Flow B — Timeline
Timeline → create post → tag member → publish → tagged profile projection.

### Flow C — Profile
Open member → posts/tagged/recognitions → message/follow.

### Flow D — Communities
Explore → community → join → publish/comment.

### Flow E — Messages
Conversation list → DM → group chat → attachment.

### Flow F — Staff
Control Center → create publication → upload media → place in Magazine module → preview → schedule/publish.

### Flow G — Auth
Google/email → eligibility → profile provisioning → first login.

---

# 12. Design acceptance gate

Do not implement full product UI until:
- mobile and desktop navigation accepted;
- Magazine Home accepted;
- Magazine card/reaction/share behavior accepted;
- Timeline post/share/tag behavior accepted;
- Profile accepted;
- Community accepted;
- Message experience accepted;
- Control Center publication/preview/layout workflow accepted;
- KDS token mapping accepted.

Use interactive prototype or coded design lab before broad feature development.
