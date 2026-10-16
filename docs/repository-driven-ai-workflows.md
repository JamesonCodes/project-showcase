# Repository-driven AI workflows

*An exploratory note on how I want to approach repeatable GTM work.*

I use “repository-driven AI workflows” as a descriptive label for keeping the materials needed to do a job together. A project folder holds context, reusable instructions, plans, scripts, inputs, outputs, QA records, logs, and lessons. The goal is to make AI-assisted work easier to repeat, inspect, and improve without rebuilding the context in every conversation. This is not a standardized framework.

My design philosophy is:

> Building a custom agent is often the wrong starting point. Before investing in orchestration, memory systems, and autonomous loops, see whether clear instructions, persistent files, scripts, and API access solve the problem. Build the simplest system that reliably gets the work done.

Unnecessary infrastructure consumes time and maintenance effort. An existing coding assistant may already supply file access, tools, scripts, and multi-step execution. Custom agents remain useful when requirements exceed those capabilities.

The value is the working process, not the folders themselves. Start with a task, define acceptable output and review points, preserve inputs, and record corrections. Scripts handle repeatable transformations; APIs supply current information or execute approved actions.

Markdown plans capture goals, decisions, status, and next steps. QA notes record checks, failures, and unresolved issues. Dated logs connect inputs, commands, outputs, and fixes so future agents can resume work without repeating failed approaches. Keep records current, distinguish planned from completed work, and remove secrets before committing logs.

Jake Van Clief and David McDermott’s **Interpretable Context Methodology (ICM)** provides a closely related architectural reference: staged folders, explicit inputs and outputs, selective context loading, and separate reusable guidance and working artifacts. It still uses agents while reducing custom orchestration. Their paper reports preliminary practitioner experience, not controlled evidence of superior performance. [ICM paper](https://arxiv.org/html/2603.16021v2), [implementation repository](https://github.com/RinDig/Interpretable-Context-Methodology).

Vercel’s **Eve** extends a directory-based approach into deployed agents: Markdown instructions and skills sit alongside TypeScript tools, with a framework providing durable execution and integrations. I see this as a possible next step when requirements justify infrastructure beyond an existing assistant. [Vercel Eve](https://vercel.com/eve).

These external examples are other teams’ work, not my implementations.

**Ad production at Anthropic.** Producing fresh ads involved repeated copy creation, character checks, and movement between tools. Anthropic describes a Claude Code workflow that combines campaign performance data, existing copy, and keywords with reusable brand, product, and advertising instructions. A marketer refines and reviews the copy before export to a Google Ads upload-ready CSV. A related Figma plugin takes headline variations and a selected creative frame to generate creative permutations. [Anthropic’s marketing workflow](https://claude.com/resources/articles/how-anthropic-uses-claude-marketing).

**Inbound qualification at Anthropic.** A small GTM team needed to qualify a large volume of interest despite incomplete data and manual Salesforce work. Clay’s customer account describes enrichment across providers, Claude-based industry classification, lead scoring, and matching personal signups to work identities. The output is enriched, standardized Salesforce records that support prioritization, with conditional opportunity and account updates. This is a vendor-reported company implementation. [Anthropic’s Clay implementation](https://www.clay.com/customers/anthropic).

**Signal-based sales at Vanta and Amplitude.** The problem is recognizing relevant account changes and opportunities. Clay reports that Vanta monitors SOC 2 announcements, compliance-related website changes, funding, and CISO job postings. Amplitude combines its product data with AI research to identify customers suited to cross-sell. The useful output is account context for prioritization and follow-up. These examples illustrate the broader pattern of inputs, interpretation, and actionable output; the source does not establish repository-based implementations. [Clay’s signal examples](https://www.clay.com/signals).

**A literal folder-based workspace.** Databar’s implementation guide addresses scattered GTM context with a proposed workspace containing ideal customer profile (ICP), positioning, voice, account notes, procedures, campaign materials, and CSV inputs and outputs. Reusable instructions and live data access support tasks such as account briefs and pipeline reviews, with results kept alongside campaign work. It is a setup guide, not evidence of a named company’s production results, and it also includes optional subagents and memory tooling. [Databar’s workspace guide](https://databar.ai/blog/article/claude-code-as-your-gtm-second-brain).

These sources illustrate useful workflow patterns. They do not prove that agents are unnecessary or that a repository-based approach always performs better. I’m exploring this approach for GTM work and will add my own implementations and evidence over time.
