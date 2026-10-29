# Personal Content Engine

I read newsletters every morning before work. Applied AI, GTM Engineering, use cases, technical breakdowns, tech news: there's always something I want to dig into. As I find more people putting out great work, my reading list keeps growing. The time I have to read it doesn't, and I end up wondering what I'm missing. It's easy to get that feeling in AI that everyone else has it figured out and you're already behind.

I also want to share more on LinkedIn and build a reputation around the things I'm learning and building. A lot of my post ideas come from projects I'm working on, but those can take time to develop into something worth sharing. They don't give me something to post every day, and I've struggled to post consistently. I'm better at setting up systems.

So I'm building a personal content engine with Codex: a workflow to help me keep up with what I'm reading, find useful connections, and turn some of them into better, more consistent LinkedIn posts. The goal is to share helpful information that other builders can learn from or try themselves, with my own perspective on what I've been learning, seeing, and reading.

| Detail | Where things stand |
| --- | --- |
| Project status | Working manual research and briefing prototype. Drafting and learning steps are written down but haven't been tried yet. |
| Documentation status | Documentation draft |
| Setup and prototype work | October 26–27, 2026 |
| Built with | Codex, AgentMail, Gmail forwarding, Markdown, JSON, Python, and Git |

## What it does

I ask Codex to run the workflow manually. It checks the newsletter inbox through AgentMail, compares messages with what it has already processed, and screens the contents for useful stories. For promising items, it follows links to the original sources.

The result is a reading brief and up to three ranked post ideas. Each idea includes possible hooks, the research behind it, and any personal input it needs from me. Then it stops so I can choose an angle and add my perspective.

Something can be worth reading without needing to become a post. That's a useful distinction to keep in the workflow.

I'm still refining the research and briefing phases to better match my taste and preferences, while leaving room for creative angles and connections I might not have thought of myself.

Once the workflow is in a better place, I plan to turn it into a recurring scheduled task in Codex. I may also break the repeatable steps out into reusable skills in the repository.

## A run so far

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

This is a working use case of the [Repository-driven AI workflows setup](../../docs/repository-driven-ai-workflows.md) I've been exploring. The context, reusable instructions, processing state, helpers, and run records live together in a project folder, so Codex can pick up the work across runs. Research and briefing are working manually; the drafting, learning, and scheduling parts are still to be tested.

This is a small workspace built with Codex's help. I set the goals, source preferences, and review boundaries, and configured subscriptions and Gmail forwarding. Codex helped organize the workspace, write the workflow instructions, retrieve and synthesize sources, generate briefs, and build the local Python helpers.

| Part | What it does |
| --- | --- |
| Context | Holds guidance about my interests, audience, and writing preferences. An `AGENTS.md` task map points Codex to the relevant files. |
| Workflow instructions | Defines research, briefing, drafting, and review steps. The last two are still untested. |
| Processing state | JSON ledgers track messages, findings, retries, and stories already surfaced, independently of unread labels. |
| Run folders | Keeps dated research notes, briefs, failures, and instructions for picking up where a run left off. |
| RSS fallback | A Python helper finds an exact article by slug or title in a public feed, rejects missing or ambiguous matches, and flags possible excerpts. |

Raw emails, article text, and intake metadata stay out of this showcase. The source repository is also omitted.

## What I've learned so far

Multiple newsletters covering the same story shouldn't turn into several separate findings or count as independent confirmation. Tracking the original story helps keep that straight.

Getting access to an article is also different from checking its claims. The research notes distinguish newsletter summaries, original articles read, and primary evidence checked. RSS can help with access, but it doesn't guarantee a complete article or corroborate what it says.

The October 26 prototype was incomplete, with gaps in intake tracking and original-source checks. The October 27 run added clearer processing state and handoffs. Keeping those earlier artifacts as historical prototypes makes it easier to see what actually changed.

## What's been checked

The local October 27 run log, research notes, brief, and processing ledgers record the nine-message intake, three original-source reads, and three post ideas described above. After the RSS follow-up, the ledger showed five messages processed, three screened, and one requiring follow-up. These records are local evidence, not public attachments.

Recorded checks include source access, duplicate detection, local links, JSON references, and focused RSS checks for exact matches, missing items, and HTML extraction.

I don't have a measured baseline for research time or publishing consistency. Review time, attributable token usage, and incremental cost haven't been measured either. So far, this shows that the manual research and briefing steps work for the recorded run; time savings and publishing outcomes are still open questions.

## What I'm trying next

Next is to review the existing brief and choose an angle, if one feels worth developing. That will let me try the drafting step with real perspective and feedback.

I also need to resolve the remaining source follow-up and verify two Gmail forwarding paths. One forwarded publication has been retrieved successfully.

Eventually I'd like an 8 a.m. America/Chicago briefing. For now, runs are manual, and there's no unattended schedule or automatic publishing.
