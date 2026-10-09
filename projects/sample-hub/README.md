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
| Deployment approach | Vercel |

## At a glance

- **Problem:** Sample submissions involved handoffs and context switching between customer conversations in Front and request creation in HubSpot.
- **Solution:** A small Front sidebar plugin that handles interpretation and setup, then lets a teammate review, correct, and explicitly submit the sample request to HubSpot.
- **Outcome:** Fewer handoffs and less context switching, with sample submissions completed inside Front.

## The problem

- **Users:** Sock Club teammates creating sample requests from customer conversations.
- **Previous workflow:** Move from Front to another system to enter recipient and shipping details, choose samples and quantities, and associate the request with a HubSpot contact.
- **Friction:** Handoffs and switching systems interrupted the task. Customer messages also needed interpretation before their details could become structured request fields.

Exact handoffs, processing time, and error rate were not recorded.

## My contribution

- **Personal responsibilities:** Directed requirements and subsequent changes, including product selections and HubSpot mappings. Reviewed changes and directed publication.
- **AI assistance:** Used Codex for implementation and maintenance: inspecting form and submission logic, editing mappings, running build checks, and committing and publishing changes.
- **Manual validation:** Tested an added product option and confirmed it worked before publication.

The original application's full division of authorship is not recorded.

## The solution

- **Trigger:** Open Sample Hub beside a Front conversation.
- **Workflow:** Enter customer details manually or use Smart-fill, choose a standard pack or custom samples, and set the requester and shipping options.
- **Human judgment:** Review and correct the editable fields, then explicitly submit. No sample request is created without that approval.
- **Output:** A HubSpot sample record and an on-screen confirmation.

## Demo

https://github.com/user-attachments/assets/0ba51a46-5c15-485b-acac-8deba9de258b

## How it works

- **Components:** A single Next.js project contains the sidebar UI and server API routes. The UI runs in Front's iframe and subscribes to conversation updates through the Front Plugin SDK. Submission requires one selected conversation.
- **Request form:** Standard packs supply preset quantities; custom sock selections calculate quantities from item counts.
- **Smart-fill:** OpenAI extracts structured fields from message text, prioritizing explicit recipient and shipping details over signatures and footers. Advanced options accept a specific message ID, with fallback to the latest eligible message and a notice. Failed extraction leaves manual entry available.
- **HubSpot integration:** The server finds an existing contact by email. A payload builder maps fields and product options, omits empty values, generates an order number, and adds shipping notes. The new record is associated with the contact and includes the Front conversation ID.
- **Credentials and context checks:** Credentials stay server-side. Both API routes check conversation and teammate identifiers through the Front Core API to address iframe cookie-authentication difficulties.
- **Error handling:** Handles missing fields, invalid context, missing contacts, and upstream API failures. After creation, it attempts a Front comment containing the HubSpot record ID when the SDK supports it. Comment failure is logged without undoing the record.
- **Diagnostics:** An optional debug panel shows context and operation logs.

## Results and evidence

The findings below come from my workflow observations, LinkedIn post, and a historical reporting chart. The post URL and underlying chart data have not yet been linked here.

| Metric or observation | Before | After or current finding | Evidence type | Measurement period | Source |
| --- | --- | --- | --- | --- | --- |
| Workflow friction | Handoffs and switching systems to complete requests | Fewer handoffs; submissions completed inside Front | Qualitative account | Not recorded | Author's LinkedIn post, supplied text |
| Attribution (secondary benefit) | Harder to trace the sample → deal → outcome conversion path | Clearer visibility into how sample requests connect to deals and their outcomes | Qualitative observation | Not recorded | Author's workflow observation |
| Sample Hub share of displayed sample records | Not recorded | Approximately 48% | AI estimate from a historical chart | Report period not recorded; discussed August 6, 2026 | “Sample Hub Percentage” |

The chart estimate used approximately 1,950 Sample Hub records out of approximately 4,095 across the displayed sources. Values were rounded. This indicates a share of recorded requests, not a before-and-after improvement or confirmed shipments. Time savings were not measured.

## Decisions and tradeoffs

- **Embed the tool in the existing workflow:** A small sidebar avoids introducing another interface teammates need to visit.
- **Keep the final decision human:** I intentionally stopped automation at the point where judgment matters, rather than automating submission end-to-end.
- **Prioritize contact association:** Requiring a HubSpot match preserves the relationship between the request and its recipient, at the cost of blocking submission until the contact exists.
- **Centralize mappings:** Separating UI labels from HubSpot values makes product-option changes easier to maintain.

## Limitations and lessons

- **Extraction coverage:** The prompt focuses on US addresses; broader address coverage is not established.
- **Scope:** The application creates sample records. It does not create missing contacts, edit sample records, or handle physical fulfillment.
- **Operations:** Operational monitoring, alerting, and deployed rate limiting are unverified. Context checks have not undergone a completed security assessment.
- **Development checks:** Historical lint checks were blocked by the Next.js and ESLint configuration. Builds required network access for Google Fonts.
- **Lesson:** The extraction, review, and submission components provide a foundation for incremental automation where appropriate. Further automation is not implemented here.

## Supporting-material links

- [Videos and hosted demos](videos/README.md)
