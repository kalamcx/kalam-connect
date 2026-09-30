# PDISC-1A Decision Lock — Magazine Home & Magazine Builder

**Decision date:** 30/09/2026  
**Status:** LOCKED  
**Authority:** Kalam Connect product owner  
**Scope:** Magazine/Home editorial behavior and staff controls

## Decision summary

The Kalam Connect **Magazine is a 100% editor-controlled member experience**.

It is not an algorithmic social feed.

Authorized staff control:
- which modules exist;
- module order;
- module visibility;
- which publications appear;
- publication order;
- card/layout treatment;
- filters;
- sorting;
- audience;
- schedule;
- placement duration;
- pinned items;
- manual overrides;
- category/theme treatment.

Automation may create or update publication drafts, but it may not silently change the Magazine layout or editorial ordering.

## Locked interaction model

### Reactions on Magazine publications
The initial reaction set is:

- Like
- Love
- Celebrate
- Support
- Wow
- Angry

A member may have one active reaction per canonical publication and may change/remove it.

Staff may disable reactions on a publication or publication type.

### Comments
Magazine publications do **not** have one global Magazine comment thread.

To discuss a Magazine publication, a member shares it to their Timeline.

Comments/replies then belong to that specific Timeline Share.

### Share
Magazine Share creates a new Timeline Share object referencing the original canonical publication.

The member may add optional commentary.

The original article/body is referenced, not duplicated.

### Tagged people
For official Magazine content, tagged/related people are automatically projected to:

- their personalized Timeline;
- their internal-public profile Tagged view;
- their profile Timeline where the projection policy permits;
- Recognitions when the relationship is recognition-related.

Tagged members receive a notification.

## Magazine Builder

The Control Center must include a visual **Magazine Builder**.

The builder supports:
- add section;
- remove section;
- rename section;
- show/hide section;
- drag/reorder section;
- select layout preset;
- select card variant;
- select manual/rule/hybrid source mode;
- build filters;
- choose sorting;
- pin items;
- manually reorder items;
- set maximum item count;
- select audience;
- set section start/end;
- set theme/accent;
- preview by device and audience;
- save draft;
- publish layout version;
- rollback to earlier layout version.

## Editorial precedence

Locked precedence:

1. explicit exclusion/visibility rules;
2. manual pinned items;
3. manual item order;
4. module query/filter;
5. module sort rule;
6. publication date tie-breaker.

No hidden engagement algorithm may override this precedence.

## Default Magazine starter composition

The initial product ships with this **editable starter layout**, not a hard-coded permanent homepage:

1. Hero Feature
2. Featured / Spotlight
3. Latest from Kalam
4. People & Recognition
5. Events & Opportunities
6. Community Highlights
7. Explore by Category

Staff may reorder, hide, duplicate where allowed, or add Custom Collection modules.

## Lock implications

This decision is upstream of:
- Timeline share behavior;
- tagged profile projections;
- Magazine analytics;
- Control Center implementation;
- publication data model;
- automation integration.

Any later change requires an explicit product decision update in this repository.

Do not silently reinterpret these rules during implementation.
