# Kalam Connect — Design System Direction

## Product character

Kalam Connect is a people/youth/community product.

The visual system should feel:
- human;
- energetic;
- editorial;
- social;
- modern;
- readable;
- friendly without becoming childish.

## Existing approved direction

Use the shared Kalam visual language:

- dark theme family: black / purple / dark blue with lavender accents;
- light theme family: lavender / pink / white with purple accents;
- other category/topic colors used intentionally;
- real people photography;
- expressive typography where appropriate;
- no AI-generated employee faces.

## Magazine vs social surfaces

Magazine:
- stronger editorial hierarchy;
- feature photography/creative;
- category color cues;
- generous whitespace;
- larger headlines.

Community/feed:
- calmer card rhythm;
- strong author identity;
- readable post body;
- obvious reactions/comments;
- mobile-first interaction density.

Messages:
- minimal distraction;
- content legibility;
- clear unread/read state;
- accessible composer.

## Kalam Design System

Kalam Connect should consume the planned Kalam Design System (KDS) rather than inventing an isolated style language.

KDS direction:
- platform-neutral tokens;
- Webflow-compatible mapping;
- React/CSS mapping;
- Figma/Core Framework compatibility where maintained.

Core categories:
- color;
- typography;
- spacing;
- radii;
- borders;
- shadows;
- motion;
- breakpoints.

## Class/token philosophy

Prefer semantic tokens:

- color-bg;
- color-surface;
- color-text-primary;
- color-text-muted;
- color-border;
- color-action-primary.

Prefer component/variant structure:

```text
button + is-primary + is-small
card + is-featured
heading + is-large
```

Avoid project debt such as:
- Button 2;
- Div Block 700;
- card-final;
- copy-of-section.

## Component foundation

Priority primitives:
- Button;
- IconButton;
- Link;
- Avatar;
- Badge;
- Input;
- Textarea;
- Select;
- Checkbox/Radio;
- Tabs;
- Tooltip;
- Dropdown;
- Modal/Sheet;
- Toast;
- Skeleton;
- Divider.

Product components:
- MagazineStoryCard;
- PostCard;
- Composer;
- CommentThread;
- ReactionBar;
- ProfileCard;
- CommunityCard;
- MemberPicker;
- NotificationItem;
- ConversationListItem;
- MessageBubble;
- PublicationStatus;
- ModerationQueueItem.

## Accessibility

Design acceptance requires:
- WCAG-oriented contrast;
- keyboard support;
- visible focus;
- reduced-motion behavior;
- readable text sizes;
- semantic heading hierarchy;
- alt text workflow;
- touch-safe targets.

## Performance

Avoid:
- heavy animation libraries for basic UI;
- uncontrolled video/large image loading;
- unnecessary glass/blur effects;
- component duplication.

Use optimized responsive images and lazy loading where appropriate.

## Implementation rule

Do not select a visual template first and then force product architecture into it.

Score candidate templates/components against:
- KDS compatibility;
- accessibility;
- performance;
- React compatibility;
- maintainability;
- responsive behavior;
- magazine/feed/community/message needs.
