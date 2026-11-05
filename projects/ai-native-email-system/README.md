# AI Native Email System

I'm building a system around Sock Club’s sales inbox that extracts customer intent, identifies the jobs inside a conversation, and decides whether to hand each job to a teammate, a specialized agent, or a team of agents to deliver the work. Agents operate within the authority earned for that job: preparing work for human review or completing it within defined limits when evidence supports bounded autonomy.

| Field | Value |
| --- | --- |
| Documentation status | Documentation draft |
| Project status | Active development. Email intake and enrichment are live, the inbox router runs in shadow mode, and the Quote Agent is in development. |
| Tools | Front, HubSpot, n8n, JavaScript, OpenRouter, Claude, OpenAI’s Decisions API, and Supabase |

## The problem

Sales and Sales Support teammates work from Front conversations, but the work inside a message often depends on information elsewhere. They need to understand the request, gather context, decide who should handle it, and follow through.

An email is only the container. A customer asking for updated artwork and pricing has raised two jobs with different outcomes and failure modes. Treating the message as one task hides those distinctions and makes it harder to measure whether the work was completed well.

*This direction also builds on findings from my [Sales Capacity Planner](../sales-capacity-planner/README.md): email jobs accounted for the largest share of estimated capacity demand. Offloading some of that work could free team capacity, improve the economics of serving accounts, and create more room for growth activity. These outcomes have not yet been measured.*

## My contribution

- **Personal responsibilities.** I’ve taken the project from the initial idea through architecture, technology selection, and implementation. I organized the system around jobs, built the shared context and routing pipeline, and used clustering to discover email intents. I’m now working out how specialist agents can take on jobs as they earn more autonomy.
- **AI assistance:** I have used Claude to analyze logged routing decisions for taxonomy gaps and gate errors.

## What I mean by AI-native

My test is to remove the AI and see what changes. In an AI-assisted inbox, a person still interprets the request and drives the work. A summary or draft helps them do it faster. In an AI-native workflow, AI performs a core step. Remove it from the system I’m building and the workflow loses its ability to identify jobs from a conversation and decide where they should go.

That’s the design I’m working toward. How much authority the system earns is a separate decision for each job. A costly or hard-to-reverse action may still call for human approval, while a job with a clear outcome and an easy recovery path may be a candidate for bounded autonomy.

## How it works

![Sales email architecture showing live intake, shadow routing, and planned job execution](diagrams/ai-native-sales-email-system.png)

### Capture and enrich emails

A Front webhook captures inbound and outbound messages. The n8n pipeline looks up the contact and account using Front and HubSpot, cleans and summarizes the message, then saves it with thread identifiers and message metadata in Supabase. A separate scheduled job generates embeddings and adds work classifications, including the task, category, work area, rationale, and classification version.

### Classify inbound email in shadow mode

I used the embeddings and work classifications from the scheduled enrichment job to study roughly 6,000 inbound messages identified as requiring action since the study began. I used a modified version of HDBSCAN, an unsupervised clustering algorithm, to find 16 groups of similar messages in those embeddings. For each cluster, I took a handful of messages nearest its center (the centroid) and used an LLM to propose an intent label based on those examples.

That gave me a starting set of intents grounded in the work customers actually asked for, without having to guess at categories up front or label thousands of messages by hand. The patterns in those clusters also helped me decide what questions the router should ask and which items to define in the Decisions API. I’m still refining the categories. I built a playground to illustrate the method using examples that contain no proprietary data. [Email Vector Lab](https://email-vector-lab.jameson-on-the-rocks.chatgpt.site/)

The Sales Inbox Router reads each new inbound message and up to three preceding messages in the thread. It makes two calls to [OpenAI’s Decisions API](https://developers.openai.com/api/docs/guides/decisions) to classify the request across 16 intents, assess urgency, and recommend who should handle it. Supabase holds the versioned intents and thresholds and records one decision per inbound email. The router records recommendations in shadow mode and leaves Front untouched.

### Hand off and complete the work

Handoff and execution are the least developed part of the system. Email intake, enrichment, and shadow routing lay the groundwork for the earned autonomy described below. I can refine routing, prepare evaluations, and develop specialist agents that can start work on their own in parallel while the development team exposes the MCP tools those workflows need to work with our internal Portal+ system.

The planned routing paths are to tag messages that need no action, hand work directly to a sales rep, or pass it to a dispatcher. The dispatcher splits requests into jobs and sends them to the appropriate specialist agents. Their outputs come together in one reply draft, flagged for review when needed. The job’s autonomy tier determines what the system can do in Front, such as draft a reply, add an internal comment, or send an approved type of reply.

The [Quote Agent](../quote-agent/README.md) is in development as a rep-started workflow. Automatic handoff from the inbox router is planned.

## Jobs and earned autonomy

I'm building a job repository to track each job's trigger, desired outcome, measures, failure modes, frequency, impact, and priority. A separate autonomy matrix records its live tier, risk and reversibility, proposed next behavior, promotion evidence, and actions that must remain human.

| Tier | Who starts and completes the work |
| --- | --- |
| 0: Manual | A person initiates, prepares, and completes the job |
| 1: Human-triggered assistance | A person initiates; AI prepares; a person completes |
| 2: System-triggered assistance | The system initiates and prepares; a person completes |
| 3: Bounded autonomy | The system initiates and completes within defined policy |

Promotion is a decision about a specific job. Frequency alone does not justify more authority. Risk, recovery, output quality, and explicit human boundaries determine what can advance. Shadow testing lets me inspect proposed behavior against real work before granting it more initiative or execution authority.

I plan to use OpenAI’s Decisions API to help choose how to handle a job based on the context of each request. The decision can adapt as the details change, while the job’s autonomy tier sets which actions are permitted and when a person needs to step in.

## Decisions and lessons

- **Discover before executing:** Shadow routing reveals workload patterns and uncertain cases while preserving human control of live work.
- **Evaluate each stage:** Separate tests for the gate and classifiers make model and prompt changes easier to assess.
- **Measure the delivered outcome:** Completing a step quickly is insufficient if the next person receives incomplete work. Autonomy needs evidence about quality as well as speed.

## Progress and evidence

The architecture records the current implementation stages. Router accuracy, end-to-end job completion, and system-wide time savings remain undocumented.

The evaluation plan includes replaying about 6,000 historical emails to tune routing and comparing shadow decisions with what reps actually did. Those comparisons would help refine intents, thresholds, and prompts. See the [evidence notes](evaluations/source-notes.md).

Because the email log and routing decisions are stored in Supabase, I can use those records to build conversation traces tailored to this workflow without buying a separate tracing tool. A trace could show the messages the router considered, the intent it identified, and who it recommended should handle the work. As dispatch and execution come online, the trace could include job handoffs and outcomes.

## Supporting materials

- [Diagrams](diagrams/README.md)
- [Evaluations and evidence register](evaluations/README.md)
- [Earlier build journal (historical background)](https://jamesoncodes.github.io/articles/ai-native-email-system.html)
