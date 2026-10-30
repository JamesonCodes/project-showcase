# Personal Content Engine

I read newsletters every morning before work: Applied AI, GTM Engineering, use cases, technical breakdowns, and tech news. My reading list keeps growing, but the time I have to read it doesn't. It's easy to get that feeling in AI that everyone else has it figured out and you're already behind.

I also want to share more on LinkedIn and build a reputation around what I'm learning and building. My projects give me post ideas, but those take time to develop into something worth sharing. I've struggled to post consistently. I'm better at setting up systems.

So I'm building a personal content engine with Codex to explore more newsletters and turn useful ideas into posts with my own perspective. I'll keep reading my core newsletters end to end; the workflow gives me a way to explore additional newsletters programmatically without adding more reading time to my routine. The goal is to share things other builders can learn from or try themselves.

| Detail | Where things stand |
| --- | --- |
| Project status | Working manual workflow from newsletter research through reviewed drafts and first LinkedIn publication. Editorial feedback has been incorporated; performance review is pending. Scheduling remains unconfigured. |
| Documentation status | Documentation draft |
| Setup and prototype work | October 26–30, 2026 |
| Built with | Codex, AgentMail, Gmail forwarding, Markdown, JSON, Python, and Git |

## What it does

I start a run manually in Codex. The workflow:

1. Checks the newsletter inbox through AgentMail and compares messages with what's already been processed.
2. Screens for useful stories and overlapping coverage, then follows promising links to original sources.
3. Produces a reading brief and up to three ranked post ideas, with possible hooks, supporting research, and any personal input needed from me.
4. Stops so I can choose an angle and add my perspective.
5. Develops and revises a draft using my feedback, preserving earlier versions. I review and publish manually.
6. Records the published post and feeds accepted editorial lessons back into the workflow. Audience performance review is the next step.

Unused ideas remain in a cross-run backlog.

I'm still refining the research and briefing phases to better match my taste and preferences, while leaving room for creative angles and connections I might not have thought of myself.

Once the workflow is in a better place, I plan to turn it into a recurring scheduled task in Codex, aiming for an 8 a.m. America/Chicago briefing. I may also break the repeatable steps out into reusable skills in the repository.

## An example run

**Sanitized example from October 30, 2026:** This summary leaves out raw emails, inbox identifiers, and personalized links while preserving the recorded counts.

| Step | October 30 manual run |
| --- | --- |
| Newsletter intake | 27 messages available; 18 new messages retrieved in full and screened |
| Original-source reading | Five selected originals read; two article-access follow-ups remained unresolved |
| Reading brief | Five findings |
| Post ideas | Three proposed idea cards, each with two possible hooks |
| Editorial selection | I chose agent identity and permissions and added my perspective |
| Drafting | Three preserved draft versions, revised through my feedback |
| Publication | First LinkedIn post published manually October 30, with a separate source comment |

I chose an angle about agent identity and permissions: who is acting, and what are they allowed to do? The post used LangChain's internal GTM agent as a concrete example, with Front's bring-your-own-agent feature as supporting context.

My feedback pushed the draft toward one focused point, shorter conversational wording, and source links in a separate comment. An AgentMail angle was saved for a future post.

## How I've put it together

This is a working use case of the [Repository-driven AI workflows setup](../../docs/repository-driven-ai-workflows.md) I've been exploring. The context, reusable instructions, processing state, helpers, and run records live together in a project folder, so Codex can pick up the work across runs.

I set the goals, source preferences, and review boundaries, and configured subscriptions and Gmail forwarding. For the first post, I selected the angle, supplied my perspective, reviewed revisions, and published. Codex supported workspace organization, workflow instructions, research and briefs, local Python helpers, drafting, revision history, and recording accepted editorial guidance.

The working repository is organized like this:

```text
personal-content-engine/
├── README.md                  # Project overview and status
├── AGENTS.md                  # Assistant task map and working rules
├── content-engine-notes.md    # Setup, decisions, and next steps
├── backlog.md                 # Carry-forward post ideas
├── context/                   # Audience, sources, and editorial guidance
├── workflow/                  # Research, brief, draft, and review contracts
├── state/                     # Processing status and story deduplication
├── runs/                      # Dated research, briefs, and execution logs
│   ├── 2026-10-26/            # Historical prototype
│   ├── 2026-10-27/            # Manual research and briefing run
│   └── 2026-10-30/            # Research, ideas, draft versions, feedback, and publication record
└── scripts/                   # RSS extraction and usage-reporting helpers
```

Reusable guidance and workflow rules stay separate from processing state and dated outputs. Raw emails, article text, intake metadata, and the source repository stay out of this showcase.

## What I've learned so far

- **Repeated coverage isn't confirmation.** Multiple newsletters covering the same story shouldn't become separate findings or count as independent evidence. Tracking the original story helps keep that straight.
- **Access isn't verification.** The research notes distinguish newsletter summaries, original articles read, and primary evidence checked. RSS helps with access, but doesn't guarantee a complete article or corroborate its claims.
- **Keep the history.** The October 26 prototype had gaps in intake tracking and original-source checks. Keeping it alongside the October 27 run makes the changes in processing state and handoffs easier to follow.
- **Reading interest and post selection are different decisions.** Liking a finding doesn't mean I want to turn it into a post. Keeping unused ideas in a backlog makes that distinction useful.
- **Editorial feedback needs to carry forward.** My revisions established preferences for shorter, conversational posts built around one point. Those preferences now live in reusable guidance.

## Results

The workflow produced its first published LinkedIn post on October 30, 2026: [“An agent that can draft an email doesn’t necessarily need permission to send it.”](https://www.linkedin.com/posts/jameson-campbell_an-agent-that-can-draft-an-email-doesnt-share-7521908533219569664-AGWF/)

This completed the first manual pass from newsletter intake through research, idea selection, drafting, revision, and publication. It also produced editorial guidance I can reuse in future runs.

Audience performance hasn't been measured yet. The first review target is November 6, 2026, at 6:19 a.m. America/Chicago, 168 hours after publication. No reminder or metrics collection is scheduled.

I plan to add available post analytics and relevant conversations here, then use repeated observations alongside my own judgment to guide future posts.

## What I'm trying next

Next is to run the workflow again using the editorial guidance from the first post, then capture the first post's results at a comparable age.

I also need to revisit two blocked article sources, verify the remaining two Gmail forwarding paths, and validate unattended access before configuring the planned 8 a.m. briefing.
