# Sample Hub

Sample Hub is a Front sidebar plugin for creating sample records in HubSpot directly from customer conversations, with optional AI assistance for filling contact and shipping details.

A sample is a hand-picked selection of socks we send to prospects and customers so they can assess the quality.

## Metadata

| Field | Value |
| --- | --- |
| Documentation status | Documentation draft |
| Project status | Deployed and being used by the team |
| My role | End-to-end ownership from inception to launch, with AI assistance for implementation and maintenance |
| Timeline | 1 week; launched January 5, 2026 |
| Tools | Next.js App Router, React, TypeScript, Front Plugin SDK and Core API, HubSpot API, OpenAI API, Git, GitHub |
| Deployment approach | Vercel |

## Problem and solution

- **Users and previous workflow:** Sock Club teammates moved from customer conversations in Front to HubSpot to create sample records with recipient, shipping, and sock-selection details. Another team processes those records and sends the samples.
- **Friction:** Handoffs and context switching interrupted the task, while customer messages needed interpretation before becoming structured request fields.
- **What changed:** Teammates can enter details manually or use Smart-fill, choose a standard pack or custom samples, and set shipping options inside Front.
- **Human judgment:** The fields remain editable. A teammate reviews, corrects, and explicitly submits the request, creating the HubSpot record and receiving an on-screen confirmation.

## My contribution

- **Personal responsibilities:** Owned the project from inception to launch, including research, planning, teammate involvement, requirements, implementation, testing, and deployment. Defined product selections and HubSpot mappings, and handled subsequent changes.
- **AI assistance:** Used Codex for implementation and maintenance: inspecting form and submission logic, editing mappings, running build checks, and committing and publishing changes.
- **Manual validation:** Tested an added product option and confirmed it worked before publication.

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

Usage figures come from internal reporting. Qualitative findings come from my workflow observations and LinkedIn post. The internal reports are not included in this repository, and the post URL has not yet been linked here.

| Metric or observation | Before | After or current finding | Evidence type | Measurement period | Source |
| --- | --- | --- | --- | --- | --- |
| Sample records created through Sample Hub | Not applicable (not yet launched) | Over 2,600 | Measured usage count | January 5–October 14, 2026 | Internal reporting |
| Workflow friction | Handoffs and switching systems to complete requests | Fewer handoffs; submissions completed inside Front | Qualitative account | Not recorded | Author's LinkedIn post, supplied text |
| Attribution (secondary benefit) | Harder to trace the sample → deal → outcome conversion path | Clearer visibility into the sample → deal → outcome path through dashboard reports | Reporting capability; qualitative improvement | Not recorded | Internal HubSpot dashboard and reports |
| Share of sample submissions via Sample Hub | Not applicable (not yet launched) | Approximately 54% | Measured usage share (rounded) | January 5–October 14, 2026 | Internal reporting |

Usage figures describe sample-record submissions, not confirmed physical shipments. Time savings were not measured.

## Decisions and lessons

- **Embed the tool in the existing workflow:** A small sidebar avoids introducing another interface teammates need to visit.
- **Keep the final decision human:** I intentionally stopped automation at the point where judgment matters, rather than automating submission end-to-end.
- **Prioritize contact association:** Requiring a HubSpot match preserves the relationship between the request and its recipient, at the cost of blocking submission until the contact exists.
- **Centralize mappings:** Separating UI labels from HubSpot values makes product-option changes easier to maintain.

- **Extraction coverage:** The prompt focuses on US addresses; broader address coverage is not established.
- **Scope:** The application creates sample records. It does not create missing contacts, edit sample records, or handle physical fulfillment.
- **Operations:** Operational monitoring, alerting, and deployed rate limiting are unverified. Context checks have not undergone a completed security assessment.
- **Development checks:** Historical lint checks were blocked by the Next.js and ESLint configuration. Builds required network access for Google Fonts.
- **Lesson:** The extraction, review, and submission components provide a foundation for incremental automation where appropriate. Further automation is not implemented here.

## Supporting materials

- [Videos and hosted demos](videos/README.md)
