# AI Native Email System

I'm building a system around Sock Club’s sales inbox that extracts customer intent, identifies the jobs inside a conversation, and decides whether to hand each job to a teammate, a specialized agent, or a team of agents to deliver the work. Agents operate within the authority earned for that job: preparing work for human review or completing it within defined limits when evidence supports bounded autonomy.

| Field | Value |
| --- | --- |
| Documentation status | Documentation draft |
| Project status | Active development resumed; refining the system around job routing, evals, and AI skills development. |
| Tools | Front, n8n, JavaScript, OpenRouter, Claude, OpenAI’s Decisions API, and Supabase |

## The problem

Sales and Sales Support teammates work from Front conversations, but the work inside a message often depends on information elsewhere. They need to understand the request, gather context, decide who should handle it, and follow through.

An email is only the container. A customer asking for updated artwork and pricing has raised two jobs with different outcomes and failure modes. Treating the message as one task hides those distinctions and makes it harder to measure whether the work was completed well.

*This direction also builds on findings from my [Sales Capacity Planner](../sales-capacity-planner/README.md): email jobs accounted for the largest share of estimated capacity demand. Offloading some of that work could free team capacity, improve the economics of serving accounts, and create more room for growth activity. These outcomes have not yet been measured.*

## My contribution

- **Personal responsibilities:** Defined jobs as the unit of work; built and refined the shared context and category-routing pipeline; created a batch analysis loop; defined the job repository and per-job autonomy framework.
- **AI assistance:** I have used Claude to analyze logged routing decisions for taxonomy gaps and gate errors.

## How it works

![Conceptual email-system pipeline from the portfolio](diagrams/system-pipeline.png)

*Conceptual architecture illustration of the intended system, not a record of current implementation coverage.*

The router hands each identified job to a teammate or specialized agents with the shared context. A human handoff can be the intended path for the job. Routing does not by itself grant an agent permission to execute; the job’s autonomy tier determines whether human completion is required.

Shared context carries the customer’s intent, desired outcome, urgency, current state, and relevant details and system identifiers. Each downstream job starts with that context rather than reconstructing the conversation. This avoids rebuilding extraction logic for every job and helps locate the source of errors.

Category routing identifies the area of work; job identification determines the specific outcomes needed within it. Uncertain cases need a review path. Outcome evaluation then informs changes to context extraction, routing, and job rules.

See [diagram notes](diagrams/README.md) for the illustration’s scope.

## Jobs and earned autonomy

I'm building a job repository to track each job's trigger, desired outcome, measures, failure modes, frequency, impact, and priority. A separate autonomy matrix records its live tier, risk and reversibility, proposed next behavior, promotion evidence, and actions that must remain human.

| Tier | Who starts and completes the work |
| --- | --- |
| 0: Manual | A person initiates, prepares, and completes the job |
| 1: Human-triggered assistance | A person initiates; AI prepares; a person completes |
| 2: System-triggered assistance | The system initiates and prepares; a person completes |
| 3: Bounded autonomy | The system initiates and completes within defined policy |

Promotion is a decision about a specific job. Frequency alone does not justify more authority. Risk, recovery, output quality, and explicit human boundaries determine what can advance. Shadow testing lets me inspect proposed behavior against real work before granting it more initiative or execution authority.

## Decisions and lessons

- **Discover before executing:** Shadow routing reveals workload patterns and uncertain cases while preserving human control of live work.
- **Evaluate each stage:** Separate tests for the gate and classifiers make model and prompt changes easier to assess.
- **Measure the delivered outcome:** Completing a step quickly is insufficient if the next person receives incomplete work. Autonomy needs evidence about quality as well as speed.

## Progress and evidence

Earlier development established a context and category-routing pipeline and a batch analysis loop for reviewing logged conversations. These are prior development milestones; current implementation coverage and evaluation results still need to be documented.

The next showcase update needs dated examples of active job paths, human handoffs, and agent execution boundaries, alongside evaluation results. Current router accuracy, end-to-end job completion, and system-wide time savings are not documented here. See the [evidence notes](evaluations/source-notes.md).

## Supporting materials

- [Diagrams](diagrams/README.md)
- [Evaluations and evidence register](evaluations/README.md)
- [Earlier build journal (historical background)](https://jamesoncodes.github.io/articles/ai-native-email-system.html)
