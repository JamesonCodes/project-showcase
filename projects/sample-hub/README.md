# Sample Hub

Sample Hub is a Front sidebar plugin for creating HubSpot sample requests directly from customer conversations, with optional AI assistance for filling contact and shipping details.

## Metadata

| Field | Detail |
| --- | --- |
| Documentation status | Documentation draft |
| Project status | Core workflow implemented; historical usage reported; current deployment status unconfirmed |
| My role | Project direction, requirements, and confirmed manual validation; used AI assistance for implementation and maintenance |
| Timeline | Start date, launch date, and total development duration not recorded |
| Tools | Next.js App Router, React, TypeScript, Front Plugin SDK and Core API, HubSpot API, OpenAI API, Git, GitHub |
| Deployment approach | Single Next.js project configured for Vercel |

## At a glance

- **Problem:** Sample requests combine information from customer conversations with structured contact, shipping, and product fields in HubSpot.
- **Solution:** A sidebar form inside Front that optionally extracts customer details, validates the request, and creates a HubSpot sample record associated with an existing contact.
- **Outcome:** The core workflow is implemented. A historical reporting chart was estimated to attribute approximately 48% of its displayed sample records to Sample Hub.

## The problem

The workflow starts with a customer conversation in Front, while sample requests are stored as structured records in HubSpot.

Users need to identify the recipient, capture the shipping address, choose samples and quantities, and associate the request with the correct contact. Information in a message also needs interpretation: a shipping address in the body may differ from an address in the sender's signature.

Sample Hub brings those steps into the conversation sidebar. Its purpose is to support sample-request creation without requiring users to leave Front to enter the request.

The previous workflow's exact steps, processing time, and error rate are not recorded.

## My contribution

I directed the project requirements and subsequent changes, including the product selections and their HubSpot mappings. I manually tested a product-option change and confirmed that it worked before requesting publication.

### AI assistance

I used Codex for implementation and maintenance assistance. Recorded work includes inspecting the form and submission logic, editing mappings, running build checks, and committing and publishing changes.

My confirmed responsibilities include requirements, review, manual validation, and directing publication. The available history does not establish a complete division of authorship for the original application.

## The solution

The user opens Sample Hub beside a single Front conversation.

They can enter customer details manually or click Smart-fill to extract contact and address information from a message. They then review the fields, choose a standard sample pack or a custom selection, set the requester and shipping options, and submit.

The backend validates the supplied Front context, checks required fields, and searches HubSpot for an existing contact by email. It creates a sample record associated with that contact and includes the Front conversation ID.

The interface confirms successful creation. When the Front SDK supports it, the application also adds a comment to the conversation containing the HubSpot record ID.

### Human judgment

Smart-fill is optional and runs only when the user clicks it. It fills an editable form rather than submitting a request automatically.

The user remains responsible for reviewing the recipient and shipping details, choosing the samples, and submitting the request.

## Demo

**Synthetic example illustrating the implemented workflow.** No real customer information is used.

A customer writes:

> Please send a standard sample pack to Jordan Lee at Example Company.
> Ship to: 123 Example Street, Austin, TX 78701.
> Contact email: [jordan@example.com](mailto:jordan@example.com).

1. The user opens Sample Hub in that Front conversation.
2. They click Smart-fill.
3. The application requests structured contact and address fields from OpenAI.
4. The user reviews the suggested values, completes any missing fields, and selects the pack, requester, and shipping options.
5. On submission, the backend searches HubSpot for `jordan@example.com`.
6. If a matching contact exists and HubSpot accepts the request, a sample record is created and associated with that contact.
7. The interface displays confirmation and attempts to add a Front comment with the new record ID.

If the contact does not exist, the backend returns an error instead of creating an unassociated sample.

This walkthrough is based on the implementation. It is not a recorded end-to-end demo.

## How it works

### Front sidebar and conversation context

The application runs inside Front's sidebar iframe and subscribes to conversation-context updates through the Front Plugin SDK.

It distinguishes between no conversation, one conversation, and multiple selected conversations. Submission requires a single-conversation context.

### Request form

The form supports:

- Client, company, email, and shipping details.
- Standard sample packs.
- Custom sock selections with quantities.
- Requester and shipping options.
- Required-field validation and submission feedback.

Standard-pack quantities are assigned from the selected pack. Custom-selection quantities are calculated from the selected item counts.

### Optional Smart-fill

Smart-fill uses conversation message text to request structured fields from OpenAI. The extraction instructions prioritize explicit shipping and recipient details in the message body over signatures and footers.

Users can supply a specific Front message ID through advanced options. If that message cannot be used, the application can fall back to the latest eligible message and display a notice.

Extraction failures leave manual entry available.

### HubSpot integration

A Next.js server route searches HubSpot contacts by the submitted email address. A matching contact is required before sample creation.

A separate payload builder:

- Maps form fields to HubSpot properties.
- Translates selectable product values into HubSpot option labels.
- Omits empty values.
- Generates a sample order number.
- Formats shipping method and shipper information into notes.

The creation route associates the sample with the matching contact and adds the Front conversation ID.

The integration creates sample records. It does not implement sample-record editing or physical fulfillment.

### Server-side credentials and context checks

HubSpot, Front, and OpenAI credentials are used server-side.

Both API routes check the supplied conversation and teammate identifiers through the Front Core API. The repository documents this approach in response to cookie-authentication difficulties inside iframes.

These checks are implemented behavior, not evidence of a completed security assessment.

### Error handling and diagnostics

The application handles missing fields, invalid Front context, missing HubSpot contacts, upstream API failures, and unsuccessful AI extraction.

An optional debug panel exposes context and operation logs for troubleshooting. A failed Front confirmation comment is logged without undoing an already-created HubSpot sample.

## Results and evidence

The evidence summary below comes from the project notes supplied for this draft. The underlying repository, historical chart, and build logs have not yet been linked in this library.

| Metric or observation | Before | After or current finding | Evidence type | Measurement period | Source |
| --- | --- | --- | --- | --- | --- |
| Sample requests created from Front | Not recorded | Sidebar, submission route, contact association, and confirmation behavior implemented | Repository inspection | Checkout reviewed in the supplied project notes | Source repository |
| Optional AI-assisted data entry | Not recorded | Manual Smart-fill populates editable contact and address fields | Repository inspection | Checkout reviewed in the supplied project notes | Form and address-parsing route |
| Sample Hub share of displayed sample records | Not recorded | Approximately 48% | AI estimate from a historical chart | Report period not recorded; discussed August 6, 2026 | “Sample Hub Percentage” |
| Manual validation | Not recorded | I confirmed that an added product option worked | Qualitative user confirmation | One maintenance test | “Add grip socks option” |
| Production build | Not recorded | Historical build checks passed when the Google Fonts network request was allowed | Recorded build results | Maintenance checks | “Add grip socks option” |

The chart estimate used approximately 1,950 Sample Hub records out of approximately 4,095 records across the displayed sources. Values were rounded, and the underlying report data was not available.

The estimate does not establish a before-and-after improvement or confirm physical shipments. Repository inspection establishes implemented behavior, while the recorded manual test covers one maintenance change. No comprehensive evaluation dataset or end-to-end test results were identified.

## Decisions and tradeoffs

### Keep request creation beside the conversation

The Front sidebar puts the form next to the source information. This supports a workflow within Front, although time savings were not measured.

### Use AI for extraction with manual submission

Smart-fill assists with interpreting message text while leaving the fields editable. The user controls when extraction runs and reviews the result before creating a record.

### Require an existing HubSpot contact

The historical plan considered optional contact association and proceeding without it. The current implementation requires a matching contact.

This preserves the contact association but prevents submission until the contact exists in HubSpot.

### Centralize field and option mappings

The payload mapping separates UI labels from HubSpot property values. Product options can be maintained without changing the overall submission workflow.

### Keep the application in one Next.js project

The sidebar UI and API routes share one project configured for Vercel. External-service credentials remain on the server.

### Treat the Front comment as a secondary action

The HubSpot record is created before the confirmation comment is attempted. Comment failure does not turn successful record creation into a failed request.

## Limitations and lessons

Smart-fill depends on the available message content and the model's extraction. Its prompt focuses on US addresses, so broader address coverage should not be assumed.

Requests require an existing HubSpot contact. The application does not create missing contacts as part of submission.

The confirmed scope ends at creating a sample record. Shipping execution and fulfillment outcomes are outside the demonstrated implementation.

Debug tools support troubleshooting, but operational monitoring and alerting are not established by the available evidence. The README recommends Vercel rate limiting; configuration in a deployed environment was not verified.

Historical lint checks were blocked by the repository's Next.js and ESLint configuration. Historical builds also required network access for Google Fonts.

The project plan is historical documentation, not a reliable completion checklist. Current behavior differs from parts of that plan, particularly contact association.

## Supporting-material links

- [Screenshots](screenshots/README.md)
- [Diagrams](diagrams/README.md)
- [Evaluations](evaluations/README.md)
- [Videos and hosted demos](videos/README.md)

Supporting assets and source-repository links have not yet been supplied. The folders above are placeholders for future material.
