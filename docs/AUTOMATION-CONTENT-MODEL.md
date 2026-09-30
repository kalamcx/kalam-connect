# Kalam Connect — Campaign, Content & Automation Model

## The missing object

The existing automation program can create copy, creative, Webflow drafts and Zoho Marketing Automation work, but those outputs need a coherent business object.

The missing object is an **Internal Communications Campaign**.

It is cross-channel and therefore must not be owned only by Kalam Connect, Webflow, or Zoho Marketing Automation.

## Authority model

### Internal Communications Campaign
Owned by approved Workflow Design + Automation operational state.

Coordinates:
- purpose;
- audience;
- source request/event;
- content package;
- creative package;
- approval;
- timing;
- channel deliveries;
- evidence.

### Kalam Connect Publication
Owned by Kalam Connect.

It is the native internal member-facing content created from an approved campaign/content package.

### Channel Delivery
Owned by the relevant adapter/provider execution.

Examples:
- Connect magazine publication;
- Connect timeline post;
- Zoho Marketing Automation email campaign/draft;
- optional Webflow draft/public mirror;
- future WhatsApp/other approved outputs.

## Canonical lifecycle

```text
Source event/request
→ Internal Communications Campaign
→ content/creative package
→ human review/approval
→ approved release package
→ channel adapters
   ├─ Kalam Connect publication
   ├─ Kalam Connect feed projection
   ├─ Zoho Marketing Automation draft/campaign
   └─ Webflow draft/mirror where still required
→ final human/provider release rules
→ evidence/reconciliation
```

## Campaign source examples

- birthday;
- anniversary;
- welcome onboard;
- Top Performers;
- recognition;
- company announcement;
- event;
- vacancy/opportunity;
- community initiative;
- internal survey;
- seasonal/internal campaign.

## Connect publication model

A single approved Connect publication can appear in more than one Connect surface.

Example:

```text
official recognition publication
   ├─ Home / Magazine
   ├─ Community timeline
   ├─ related member profiles
   └─ related community
```

Do not create duplicate content rows solely because the same story is shown in multiple surfaces.

Use placement/projection metadata.

## Publication input package

SOLO/Automation should be able to send a versioned approved package containing:

- campaign_ref;
- content_package_ref;
- publication_type;
- title;
- summary;
- body;
- category;
- related_people[];
- related_community if any;
- media[];
- audience;
- publish/schedule instruction;
- approval reference/state;
- source evidence references;
- idempotency_key;
- correlation_id;
- version.

## Approval

External/cross-channel automation must not bypass the approved review policy.

Connect supports statuses:

`draft → review → scheduled → published → archived`.

Automation may safely create/update a draft/review object before human approval when the workflow contract allows preview creation.

Publication/release requires the appropriate approved authority.

## Multi-person recognition

Top Performers and similar content must support:

```text
1 publication
→ 1..N people
```

Do not model recognition as one post per person unless the campaign explicitly requires separate individual posts.

## People imagery

Never AI-generate an employee's face as a substitute for the verified person image.

Where campaign creative includes a person:
- resolve the approved verified profile image;
- use it according to media/privacy rules;
- preserve source/reference metadata.

## Creative outputs

A Connect campaign package may include:

1. main magazine/social creative;
2. email/category creative;
3. thumbnail/card creative.

The design workflow can evolve, but the publication contract should reference assets by stable IDs/URLs and roles rather than provider-specific internal steps.

## Webflow transition

If Webflow continues to receive campaign drafts:

- treat it as a delivery adapter;
- record the Webflow item ID/URL as a delivery receipt;
- do not use Webflow CMS as Connect's member/content database;
- do not require a Webflow draft for a native Connect publication to exist.

## Zoho Marketing Automation

Zoho MA owns outbound email journey/campaign delivery.

Automation should:
- create/update the appropriate draft/campaign after the workflow release gate;
- preserve provider campaign ID;
- return status/receipt;
- reconcile send/publish evidence.

Connect may display a staff-level delivery status but must not become the Zoho MA execution engine.

## Automation responsibilities

Automation repo should eventually expose capabilities such as:

- internal_campaign.create_or_update
- internal_campaign.build_release_package
- connect_publication.create_or_update
- connect_publication.release
- zoho_ma_campaign.create_or_update
- webflow_delivery.create_or_update
- campaign.reconcile

Exact names are owned by the Automation capability catalog.

## Failure model

Partial channel failure must not corrupt the campaign.

Example:

```text
Connect publication = success
Zoho MA draft = failed
Webflow mirror = success
```

Campaign status becomes degraded/partial with a retryable delivery exception.

Do not roll back successful native Connect publishing automatically unless the business workflow explicitly requires atomic release.

## Evidence

Each delivery should preserve:
- campaign_ref;
- channel;
- provider/object ref;
- status;
- execution/correlation ID;
- timestamp;
- error code where relevant;
- final URL/reference where relevant.

This lets SOLO and SIA measure the experiment without making Connect or n8n the evidence authority for unrelated channels.
