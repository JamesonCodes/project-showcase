# Personal Content Engine

I read newsletters every morning before work: Applied AI, GTM Engineering, use cases, technical breakdowns, and tech news. My reading list keeps growing, but the time I have to read it doesn't. It's easy to get that feeling in AI that everyone else has it figured out and you're already behind.

I also want to share more on LinkedIn and build a reputation around what I'm learning and building. My projects give me post ideas, but those take time to develop into something worth sharing. I've struggled to post consistently. I'm better at setting up systems.

So I'm building a personal content engine with Codex to explore more newsletters and turn useful ideas into posts with my own perspective. I'll keep reading my core newsletters end to end; the workflow gives me a way to explore additional newsletters programmatically without adding more reading time to my routine. The goal is to share things other builders can learn from or try themselves.

| Detail | Where things stand |
| --- | --- |
| Project status | Working manual research and briefing prototype. Drafting and learning steps are written down but haven't been tried yet. |
| Documentation status | Documentation draft |
| Setup and prototype work | October 26–27, 2026 |
| Built with | Codex, AgentMail, Gmail forwarding, Markdown, JSON, Python, and Git |

## What it does

I start a run manually in Codex. The workflow:

1. Checks the newsletter inbox through AgentMail and compares messages with what's already been processed.
2. Screens for useful stories and overlapping coverage, then follows promising links to original sources.
3. Produces a reading brief and up to three ranked post ideas, with possible hooks, supporting research, and any personal input needed from me.
4. Stops so I can choose an angle and add my perspective before drafting. Publishing is manual.

Something can be worth reading without needing to become a post.

I'm still refining the research and briefing phases to better match my taste and preferences, while leaving room for creative angles and connections I might not have thought of myself.

Once the workflow is in a better place, I plan to turn it into a recurring scheduled task in Codex, aiming for an 8 a.m. America/Chicago briefing. I may also break the repeatable steps out into reusable skills in the repository.

## An example run

**Sanitized example from October 27, 2026:** This summary leaves out raw emails, inbox identifiers, and personalized links while preserving the recorded counts.

| Step | October 27 manual run |
| --- | --- |
| Newsletter intake | All nine available issues retrieved and screened for overlapping coverage |
| Original-source reading | Three selected originals read |
| Reading brief | Three findings |
| Post ideas | Three ranked ideas, each with two possible hooks |
| Drafting and publication | No idea selected, draft generated, or post published |

One idea explored how an agent integration should preserve the business checks already enforced by a normal application interface. The brief asked me for a real project example before taking that angle further.

Some sources were inaccessible, so the workflow left them as follow-ups. Later, a public RSS feed provided an exact match for one blocked article. That follow-up was recorded separately, keeping the original morning brief intact.

## How I've put it together

This is a working use case of the [Repository-driven AI workflows setup](../../docs/repository-driven-ai-workflows.md) I've been exploring. The context, reusable instructions, processing state, helpers, and run records live together in a project folder, so Codex can pick up the work across runs.

I set the goals, source preferences, and review boundaries, and configured subscriptions and Gmail forwarding. Codex helped organize the workspace, write the workflow instructions, retrieve and synthesize sources, generate briefs, and build the local Python helpers.

The working repository is organized like this:

```text
personal-content-engine/
├── README.md                  # Project overview and status
├── AGENTS.md                  # Assistant task map and working rules
├── content-engine-notes.md    # Setup, decisions, and next steps
├── context/                   # Audience, sources, and editorial guidance
├── workflow/                  # Research, brief, draft, and review contracts
├── state/                     # Processing status and story deduplication
├── runs/                      # Dated research, briefs, and execution logs
│   ├── 2026-10-26/            # Historical prototype
│   └── 2026-10-27/            # Manual research and briefing run
└── scripts/                   # RSS extraction and usage-reporting helpers
```

Reusable guidance and workflow rules stay separate from processing state and dated outputs. Raw emails, article text, intake metadata, and the source repository stay out of this showcase.

## What I've learned so far

- **Repeated coverage isn't confirmation.** Multiple newsletters covering the same story shouldn't become separate findings or count as independent evidence. Tracking the original story helps keep that straight.
- **Access isn't verification.** The research notes distinguish newsletter summaries, original articles read, and primary evidence checked. RSS helps with access, but doesn't guarantee a complete article or corroborate its claims.
- **Keep the history.** The October 26 prototype had gaps in intake tracking and original-source checks. Keeping it alongside the October 27 run makes the changes in processing state and handoffs easier to follow.

## Results

TBD. I'm still refining the workflow and haven't started publishing posts through it yet.

Once I do, I plan to share LinkedIn post analytics here alongside the posts and what I was trying with each one. I'll track how consistently I'm posting and which topics and angles get a response.

Those analytics will also feed into the workflow's review step, helping guide future topics, hooks, and formats based on what resonates. I'll use those patterns alongside my own judgment to shape new posts and test whether the results repeat.

## What I'm trying next

Next is to review the existing brief and choose an angle, if one feels worth developing. That will let me try the drafting step with real perspective and feedback.

I also need to resolve the remaining source follow-up and verify two Gmail forwarding paths. One forwarded publication has been retrieved successfully.
