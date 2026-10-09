# Sample Hub

Sample Hub is a Front sidebar plugin for creating HubSpot sample requests directly from customer conversations, with optional AI assistance for filling contact and shipping details.

## Metadata

| Field | Value |
| --- | --- |
| Documentation status | Documentation draft |
| Project status | Core workflow implemented; historical usage reported; current deployment status unconfirmed |
| My role | Project direction, requirements, and confirmed manual validation; used AI assistance for implementation and maintenance |
| Timeline | 1 week |
| Tools | Next.js App Router, React, TypeScript, Front Plugin SDK and Core API, HubSpot API, OpenAI API, Git, GitHub |
| Deployment approach | Single Next.js project configured for Vercel |

## At a glance

- **Problem:** Sample submissions involved handoffs and context switching between customer conversations in Front and request creation in HubSpot.
- **Solution:** A small Front sidebar plugin that handles interpretation and setup, then lets a teammate review, correct, and explicitly submit the sample request to HubSpot.
- **Outcome:** Fewer handoffs and less context switching, with sample submissions completed inside Front. A historical chart estimate attributed approximately 48% of its displayed sample records to Sample Hub.

## The problem

- **Users:** Sock Club teammates creating sample requests from customer conversations in Front.
- **Workflow:** Identify the recipient, capture shipping details, choose samples and quantities, and associate the request with the correct HubSpot contact.
- **Friction:** Handoffs between people and switching systems interrupted the task. Conversation details also needed interpretation before becoming structured HubSpot fields, especially when shipping details differed from the sender's signature.
- **Previous workflow:** Move from the customer conversation in Front to another system to finish the sample submission. Exact handoffs, processing time, and error rate were not recorded.

Sample Hub brings request creation into the conversation sidebar so users can complete the intake without leaving Front.

## My contribution

- **Personal responsibilities:** Directed requirements and subsequent changes, including product selections and HubSpot mappings. Reviewed changes and directed publication.
- **AI assistance:** Used Codex for implementation and maintenance, including inspecting form and submission logic, editing mappings, running build checks, and committing and publishing changes.
- **Manual validation:** Tested an added product option and confirmed it worked before requesting publication.

These responsibilities are confirmed in the project notes; the original application's full division of authorship is not recorded.

## The solution

- **Trigger:** Open Sample Hub beside a single Front conversation.
- **Workflow:** Enter customer details manually or use Smart-fill, review the fields, choose a standard pack or custom samples, set the requester and shipping options, and submit.
- **Validation:** The backend checks Front context and required fields, then searches HubSpot for an existing contact by email.
- **Output:** A HubSpot sample record associated with that contact and the Front conversation ID. The interface confirms creation and, when supported by the Front SDK, adds a conversation comment with the record ID.
- **Human judgment:** Smart-fill runs only when clicked and fills editable fields. A teammate reviews the recipient, address, and selections, corrects edge cases, and makes the final call. No sample request is created without explicit human submission.

## Demo

### Video walkthrough

https://github.com/user-attachments/assets/0ba51a46-5c15-485b-acac-8deba9de258b

### Example workflow

**Synthetic example:** The written walkthrough below uses fictional customer details.

> Please send a standard sample pack to Jordan Lee at Example Company.
>
> Ship to: 123 Example Street, Austin, TX 78701.
>
> Contact email: jordan@example.com.

1. **Input:** Open Sample Hub in the conversation and click Smart-fill. OpenAI extracts structured contact and address fields from the message.
2. **Review and submission:** Review the suggested values, complete missing fields, and choose the pack, requester, and shipping options. Submit the form; the backend searches HubSpot for `jordan@example.com`.
3. **Outcome:** If the contact exists and HubSpot accepts the request, the sample record is created and associated with the contact. The interface confirms creation and attempts to add a Front comment with the record ID.

If the contact is missing, the backend returns an error instead of creating an unassociated sample.

## How it works

- **Components:** One Next.js project configured for Vercel contains the sidebar UI and server API routes. The UI runs in Front's iframe and subscribes to conversation updates through the Front Plugin SDK.
- **Conversation context:** The application distinguishes no conversation, one conversation, and multiple selected conversations. Submission requires a single conversation.
- **Request form:** Collects client, company, email, shipping details, requester, and shipping options. Users choose a standard pack or custom socks with quantities. Standard-pack quantities come from the pack; custom quantities are calculated from item counts.
- **Smart-fill:** Sends message text to OpenAI for structured extraction. Explicit recipient and shipping details in the body take priority over signatures and footers. Advanced options accept a specific message ID; an unusable message can fall back to the latest eligible one with a notice. Manual entry remains available if extraction fails.
- **HubSpot integration:** A server route finds an existing contact by email. A payload builder maps form fields to HubSpot properties and option labels, omits empty values, generates an order number, and adds shipping method and shipper details to notes. The creation route associates the sample with the contact and includes the Front conversation ID.
- **Credentials and context checks:** Front, HubSpot, and OpenAI credentials stay server-side. Both API routes check conversation and teammate identifiers through the Front Core API, an approach documented in response to iframe cookie-authentication difficulties. These checks do not constitute a completed security assessment.
- **Error handling:** Handles missing fields, invalid Front context, missing contacts, upstream API failures, and failed extraction. A failed Front confirmation comment is logged without undoing the HubSpot record.
- **Diagnostics:** An optional debug panel shows context and operation logs. Operational monitoring and alerting are not established in the available evidence.

The integration creates sample records; record editing and physical fulfillment are outside its implemented scope.

## Results and evidence

The evidence summary below comes from the supplied project notes and my LinkedIn post about the tool. The underlying repository, historical chart, build logs, and post URL have not yet been linked in this library.

| Metric or observation | Before | After or current finding | Evidence type | Measurement period | Source |
| --- | --- | --- | --- | --- | --- |
| Sample requests created from Front | Not recorded | Sidebar, submission route, contact association, and confirmation behavior implemented | Repository inspection | Checkout reviewed in the supplied project notes | Source repository |
| Optional AI-assisted data entry | Not recorded | Manual Smart-fill populates editable contact and address fields | Repository inspection | Checkout reviewed in the supplied project notes | Form and address-parsing route |
| Workflow friction | Handoffs and switching systems to complete requests | Fewer handoffs; sample submissions completed inside Front | Qualitative account | Not recorded | Author's LinkedIn post, supplied text |
| Sample Hub share of displayed sample records | Not recorded | Approximately 48% | AI estimate from a historical chart | Report period not recorded; discussed August 6, 2026 | “Sample Hub Percentage” |
| Manual validation | Not recorded | I confirmed that an added product option worked | Qualitative user confirmation | One maintenance test | “Add grip socks option” |
| Production build | Not recorded | Historical build checks passed when the Google Fonts network request was allowed | Recorded build results | Maintenance checks | “Add grip socks option” |

The chart estimate used approximately 1,950 Sample Hub records out of approximately 4,095 records across the displayed sources. Values were rounded, and the underlying report data was not available.

The estimate does not establish a before-and-after improvement or confirm physical shipments. Repository inspection establishes implemented behavior, while the recorded manual test covers one maintenance change. No comprehensive evaluation dataset or end-to-end test results were identified.

## Decisions and tradeoffs

- **Stay beside the conversation:** Keep the UI small and embed assistance in the workflow teammates already use. The request can be completed inside Front; time savings were not measured.
- **Stop automation at human judgment:** I intentionally kept review and submission with a person. AI handles interpretation and setup; the teammate corrects edge cases and approves the request.
- **Require an existing contact:** The historical plan allowed optional association; the implementation requires a HubSpot match. This preserves the association but blocks requests until the contact exists.
- **Centralize mappings:** Separate UI labels from HubSpot values so product options can change without changing the submission workflow.
- **Use one Next.js project:** Keep the UI and API routes together, with external-service credentials on the server.
- **Make the Front comment secondary:** Create the HubSpot record first. Comment failure does not turn successful record creation into a failed request.

## Limitations and lessons

- **Extraction coverage:** Smart-fill depends on message content and model output. Its prompt focuses on US addresses; broader address coverage is not established.
- **Contact requirement:** Requests need an existing HubSpot contact. Submission does not create missing contacts.
- **Fulfillment scope:** The workflow ends at sample-record creation. Shipping execution and fulfillment outcomes are outside the demonstrated implementation.
- **Operations:** Deployed rate limiting was not verified. The source README recommends Vercel rate limiting; operational monitoring and alerting are not established.
- **Development checks:** Historical lint checks were blocked by the Next.js and ESLint configuration. Builds required network access for Google Fonts.
- **Documentation:** The historical project plan is not a completion checklist. Current behavior differs from it, particularly contact association.
- **Lesson:** Human-in-the-loop assistance can remove workflow friction without automating the final decision. These components also provide a foundation for incremental automation where appropriate; further automation is not implemented here.

## Supporting-material links

- [Videos and hosted demos](videos/README.md)
