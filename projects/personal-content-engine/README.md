# Personal Content Engine

An AI-assisted workflow that turns newsletter research into evidence-backed reading briefs and potential LinkedIn post angles, with human review before drafting and publication.

| Field | Details |
| --- | --- |
| Documentation status | Documentation draft |
| Project status | Working manual research and briefing prototype; drafting and learning workflows defined but not yet exercised |
| My role | Project owner, workflow designer, and editorial decision-maker, working with Codex |
| Timeline | Setup and prototype work recorded October 26–27, 2026; experiment start and end dates not set |
| Tools | Codex, AgentMail plugin/MCP access, Gmail forwarding, Markdown, JSON, Python standard library, Git |

## At a glance

- **Problem:** I wanted a repeatable way to learn from GTM Engineering and Applied AI sources and turn useful findings into content without losing source context or inventing personal experience.
- **Solution:** A staged workspace for research, briefing, drafting, and review, supported by persistent intake state and explicit human checkpoints.
- **Outcome:** A manual run screened nine newsletter issues, read three selected original sources, and produced three ranked post ideas. A later RSS fallback recovered another blocked article. Scheduled delivery and publishing outcomes remain untested.

## The problem

This is a personal workflow built around my own research and publishing decisions. The intended content audience includes GTM and RevOps hiring managers, collaborators, and other builders.

The challenge is more than summarizing newsletters. Several publications can cover the same story, an email can omit important evidence, and an interesting article does not automatically make a useful post. A proposed angle may also need personal experience that the system cannot supply.

I wanted the workflow to preserve those distinctions while keeping editorial judgment with me.

A measured baseline for research time, review effort, and publishing consistency was not recorded.

## My contribution

I set the project goals, audience, positioning, source preferences, and review boundaries. I chose a newsletter-first approach and approved the staged workspace structure.

I also configured newsletter subscriptions and Gmail forwarding for sources that I was having difficulty subscribing to through the AgentMail address. One forwarded publication was verified through retrieval; two other forwarding paths remained unverified.

Codex assisted with workspace organization, workflow documentation, source retrieval and synthesis, brief generation, processing ledgers, and local Python helpers. The implementation was developed with AI assistance. I do not present the generated artifacts or helper code as work completed without that assistance.

The recorded validation includes source-access checks, duplicate detection, local link and JSON/reference checks, and focused RSS extraction checks. No additional human collaborators are recorded.

I retain responsibility for selecting an angle, supplying personal perspective, reviewing drafts, and publishing.

## The solution

The implemented workflow starts with a manual request in Codex.

1. Read the relevant guidance and current run log.
2. List received newsletter messages and compare them with the processing ledger.
3. Retrieve bodies, screen relevance, and identify duplicate stories.
4. Read promising original sources and record access gaps.
5. Produce a reading brief and up to three ranked post ideas.
6. Stop for my selection and perspective before drafting.

The output separates what is worth reading from what might be worth posting. Each proposed idea connects to research findings and identifies missing personal input.

Drafting and editorial learning have documented handoffs, but neither had been exercised with an actual selected angle or published post in the recorded runs.

## Demo

**Sanitized example, summarized from the October 27 manual run.** Raw emails, inbox identifiers, and personalized links are omitted. The summary preserves the recorded workflow and output counts.

**Input →** Nine available newsletter issues, existing brand guidance, and a prior prototype brief.

**System behavior →** The workflow retrieved all nine bodies, screened them, identified overlapping coverage, and read three selected originals. It recorded inaccessible sources as follow-ups instead of treating their claims as verified.

**Output →** A reading brief with three findings and three ranked post ideas, each with two proposed hooks and a request for relevant personal perspective.

One idea asked how an agent integration should preserve the business checks already enforced by a normal application interface. The brief asked me for a real project example before developing that angle.

**Outcome →** A reviewable research and ideation artifact. No selection, draft, or publication was recorded.

During a later follow-up, an exact article match in a public RSS feed resolved one source-access blocker. The original morning brief was preserved rather than silently rewritten.

No screenshots or hosted demo are included.

## How it works

### Context and stage contracts

Reusable guidance lives in `context/`. Separate workflow files define research, briefing, drafting, and review requirements.

An `AGENTS.md` task map directs the assistant to relevant files. Approved guidance stays separate from historical drafts and untested hypotheses. This is a context-management design choice, not a measured performance improvement.

### Read-only newsletter intake

AgentMail provides message listing and full-body retrieval through its plugin. Gmail forwarding supports some subscriptions.

Processing state is independent of unread labels. For the small inbox, the workflow lists all available messages and compares IDs against the ledger, helping catch forwarded or backfilled issues with older original dates.

### Persistent state

Two JSON files serve different purposes:

- `state/messages.json` records processing status, retry reasons, and next actions.
- `state/findings.json` tracks canonical stories, evidence references, and prior surfacing.

Message states distinguish new, screened, follow-up needed, processed, and failed items. Story-level deduplication prevents repeated newsletter coverage from becoming multiple independent findings.

### Evidence and access failures

Research records distinguish newsletter-level evidence, original articles read, and primary evidence checked.

Blocked sources remain explicit gaps. A Python helper can extract an exact article from a public RSS feed using its slug or title. It rejects missing or ambiguous matches, retains source metadata, and flags possible excerpt markers. RSS extraction does not guarantee completeness or provide independent corroboration.

### Human review and operational records

Dated run folders contain research, briefs, QA, failures, and resume instructions.

The workflow stops before drafting until I select an angle and provide needed perspective. Publication remains manual.

Raw emails, extracted article text, credentials, and personal analytics belong in ignored local storage. No unattended schedule or automatic publishing is configured.

## Results and evidence

The sources below are local workspace records, not public attachments. The counts and checks are summarized from those records; raw intake metadata, article text, and processing ledgers are not included in this showcase.

| Metric or observation | Before | After | Evidence type | Measurement period | Source |
| --- | --- | --- | --- | --- | --- |
| Newsletter coverage in the manual run | Not recorded | Nine available issues listed and all nine bodies retrieved | Recorded execution count | October 27, 2026, intake snapshot at 06:05:40 -05:00 | October 27 run log |
| Original-source reading | Not recorded | Three selected originals read during the morning run | Recorded execution count | October 27 morning run | Research artifact and run log |
| Editorial output | Not recorded | Three ranked ideas, each with two proposed hooks | Artifact inspection | October 27 morning run | Brief |
| Processing state after the RSS follow-up | No trustworthy prior ledger | Five processed, three screened, one requiring follow-up | Recorded state summary | October 27, after source recovery | Run log and processing ledgers |
| Blocked-source recovery | Exact GitHub marketing article inaccessible through the attempted article route | Matching RSS article extracted and read; 1,431 words reported | Retrieval record and qualitative completeness review | October 27, 2026, 11:37:02 UTC | RSS follow-up entry |
| RSS helper checks | Not recorded | Exact-match, missing-item, and HTML extraction checks recorded as passed | Focused functional checks | October 27, 2026 | Run log |

These results demonstrate manual execution and artifact production. They do not establish reliable unattended operation, editorial quality, time savings, or audience growth.

Review time, attributable token usage, and actual incremental cost were not measured. The setup and manual run shared execution context, so I excluded them from a briefing-only token baseline.

The proposed 30–60 day experiment and goal of having 100 people associate my name with GTM Engineering / Applied AI are intentions, not achieved results. No experiment launch date or recognition measurement is recorded.

## Decisions and tradeoffs

| Decision | Reason and tradeoff |
| --- | --- |
| Start with existing Codex access and AgentMail | Test workflow usefulness before adding custom infrastructure. Unattended access still needs validation. |
| Use newsletters as the initial intake channel | Keep research bounded while allowing selected original-source checks. Independent social-feed and YouTube monitoring are deferred. |
| Separate reading interest from posting interest | A useful finding can remain research without becoming a forced content idea. |
| Track processing independently of unread labels | Preserve retry and reuse decisions without changing the inbox. This adds local state to maintain. |
| Deduplicate by original story identity | Repeated coverage should not inflate finding counts or appear to corroborate a claim independently. |
| Require selection before drafting | Preserve my judgment and prevent invented personal experience. This creates an intentional manual handoff. |
| Use public RSS as an access fallback | Recover available original text without treating access success as proof of completeness. |
| Defer token measurement until runs are isolated | Avoid assigning mixed setup work to recurring operating costs. This leaves current costs unmeasured. |

## Limitations and lessons

The strongest current evidence is for manual research and briefing. The project has not completed the full path from intake to selected draft, publication, and performance review.

The October 26 prototype was incomplete: it lacked comprehensive intake state and original-source verification. It remains labeled as a historical prototype rather than a completed run or accepted writing example.

The October 27 work made the handoffs more explicit. Source access, research completion, editorial selection, and publication approval are separate states.

A successful retrieval also does not establish the underlying claim. Likewise, duplicate coverage is not independent corroboration.

These are implementation lessons and safeguards. No performance-derived editorial lessons have been accepted yet, and the context structure has not been compared against an alternative in a controlled evaluation.

## Current state and next steps

The next useful step is to review the existing brief and select an angle, if any. That would allow the drafting handoff to be tested with real perspective and feedback.

Other open work includes resolving the remaining source follow-up, verifying two forwarding paths, and validating the complete manual workflow before scheduling.

The target briefing time is 8 a.m. America/Chicago. Publishing cadence, review-time budget, and spending limit remain undecided.

The source repository is not included in this showcase.
