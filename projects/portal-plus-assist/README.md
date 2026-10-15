# Portal+ Assist

![Portal+ Assist cover showing an inbox alongside Portal+ project and design-request context](screenshots/cover.jpg)

Portal+ Assist is an internal Front plugin that brings Portal+ sales workflows into customer conversations, using AI to prepare work for human review and approval.

## Metadata

| Field | Value |
| --- | --- |
| Documentation status | Documentation draft |
| Project status | {{Confirm current deployment status and which capabilities are live}} |
| My role | {{Describe my ownership and responsibilities}} |
| Timeline | {{Provide development duration and launch dates}} |
| Tools | Front, Portal+; {{Add the implementation stack and AI services}} |

## Problem and solution

- **Users and previous workflow:** Sales and sales support work primarily in Front, where customer conversations progress deals. Creating quotes, submitting design and revision requests, building carts, and processing purchase orders require moving into other systems.
- **Friction:** Teammates copy, paste, and transcribe context from email threads and PDFs. Strategic Accounts also depend on handoffs between roles, adding coordination work even when the customer's intent is clear.
- **Product approach:** Bring common Portal+ workflows into Front so teammates can initiate internal actions where the context already exists. AI interprets that context and prepares suggested actions.
- **Human judgment:** A teammate reviews, edits, and approves the prepared work. Nothing executes without explicit human approval; sales and sales support retain accountability.

## My contribution

- **Personal responsibilities:** {{Describe what I researched, designed, built, and launched}}
- **Collaborators:** {{Describe others' contributions, if applicable}}
- **AI assistance:** {{Describe development assistance separately from AI used by the product}}
- **Validation:** {{Describe actual testing and teammate review}}

## Demo

{{Add a hosted walkthrough or screenshots of a confirmed live capability. Show the conversation context, prepared action, human review, and approved outcome. Label examples as real, sanitized, or synthetic.}}

## How it works

- **Product structure:** One Front plugin exposes multiple Portal+ capabilities, each organized around a repeatable sales workflow.
- **Workflow pattern:** Interpret context → prepare a suggested action → human review and editing → explicit approval → execution.
- **Capability scope:** {{List implemented capabilities and distinguish live workflows from planned work. The product brief identifies quotes, new design and revision requests, carts, and purchase orders as workflow needs; it does not establish that all are implemented.}}
- **Components and integrations:** {{Describe how Front context reaches the plugin and how approved actions are submitted to Portal+}}
- **Error handling and monitoring:** {{Describe implemented validation, failure handling, diagnostics, and recovery}}

## Results and evidence

The intended benefits are less context switching, fewer manual transfers and handoffs, and more time for selling. These are product goals; measured outcomes have not yet been added to this case study.

| Metric or observation | Before | After or current finding | Evidence type | Measurement period | Source |
| --- | --- | --- | --- | --- | --- |
| Workflow friction | Context switching, manual transcription, and handoffs between roles | {{Add observed changes for a confirmed live capability}} | Qualitative problem account; outcome pending | Not recorded | Author's original product brief |

{{Add supported usage figures, measured results, team-informed estimates, or qualitative feedback with their sources and periods.}}

## Decisions and lessons

- **Optimize for momentum:** Keep common workflows close to customer conversations. Portal+ remains the place for full control and complex exceptions.
- **Use a consistent approval model:** Each capability follows the same preparation, review, and approval pattern so teammates retain control as workflows expand.
- **Focus on frequent work:** Prioritize common, repeatable actions rather than attempting every edge case.
- **Preserve ownership:** Remove repetitive transfer and setup work while retaining sales and sales support expertise. Replacing these roles is outside the product's scope.
- **Bound automation:** AI assists with interpretation and suggestions. Autonomous execution and final decisions are outside the product's scope.
- **Lessons:** {{Add lessons from implementation and actual team use}}

## Supporting materials

- {{Add links to available demos, diagrams, screenshots, or evidence as they are added}}
- **Source repository:** {{Link the existing source repository if shareable}}
- **Related case study:** [AI Native Email System](../ai-native-email-system/README.md)
