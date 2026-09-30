# PDISC-1B Decision Lock — Publication Types & Field Matrix

**Decision date:** 30/09/2026  
**Status:** LOCKED  
**Authority:** Kalam Connect product owner

## Locked decisions

1. Existing Webflow/Kalam Connect data is the migration baseline.
2. Shared Kalam People remains the people authority.
3. Categories are editorial taxonomy, not application behavior.
4. Official publication behavior uses:
   - `publication_type`
   - optional controlled `publication_subtype`
   - one or more categories.
5. Initial publication types:
   - story
   - announcement
   - recognition
   - people_milestone
   - event
   - opportunity
   - poll
   - community_feature
6. Existing 12 Connect categories remain initial categories and map into the above behavior types.
7. Birthday/Anniversary/Promotion/Welcome/Celebration are people-milestone subtypes.
8. Top Performers/Leader of the Month/general Recognition are recognition subtypes.
9. Training/Tips use story behavior unless a specific item is actually an event.
10. Vacancy uses opportunity behavior.
11. People relationships are normalized and carry relationship semantics.
12. Media is normalized by reusable asset + role.
13. Form/CTA behavior is normalized into publication actions.
14. Type-specific fields use controlled `type_data` initially; highly queryable/independent domains may later receive dedicated tables.
15. Legacy fields are migrated losslessly using native destinations plus `legacy_data`.
16. Automation and staff operate the same native publication object.
17. Automation may draft/populate source-backed fields but cannot bypass editorial approval or overwrite reviewed human work silently.

Canonical full specification:

`docs/PUBLICATION-TYPE-FIELD-MATRIX.md`

Migration baseline:

`docs/SCHEMA-BASELINE-LEGACY-MAPPING.md`

Do not reopen these decisions during implementation without an explicit owner product decision.
