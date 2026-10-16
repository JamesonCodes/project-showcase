# Repository-driven AI workflows

*An exploratory note on how I want to approach repeatable GTM work.*

I use “repository-driven AI workflows” as a descriptive label for keeping the materials needed to do a job together. A project folder holds context, reusable instructions, scripts, inputs, outputs, and lessons. The goal is to make AI-assisted work easier to repeat, inspect, and improve without rebuilding the context in every conversation. This is not a standardized framework.

My design philosophy is:

> Building a custom agent is often the wrong starting point. Before investing in orchestration, memory systems, and autonomous loops, see whether clear instructions, persistent files, scripts, and API access solve the problem. Build the simplest system that reliably gets the work done.

Unnecessary agent infrastructure can consume time and maintenance effort without improving the outcome. An existing coding assistant may already provide the ability to read files, use tools, run scripts, and work through multiple steps. Custom agents remain useful when the work justifies them, such as a recurring process that needs dedicated execution, state management, or integrations beyond the existing assistant.

The value is the working process, not the folders themselves. I would start with one concrete task, define acceptable output and review points, preserve the inputs, and record corrections as reusable guidance. Scripts handle repeatable transformations; API access supplies current information or executes approved actions. Outputs and results make the next iteration easier to evaluate. A tidy directory alone does none of that.

The following external examples help make the pattern tangible. They are other teams’ work, not my implementations.

**Ad production at Anthropic.** Producing fresh ads involved repeated copy creation, character checks, and movement between tools. Anthropic describes a Claude Code workflow that combines campaign performance data, existing copy, and keywords with reusable brand, product, and advertising instructions. A marketer refines and reviews the copy before export to a Google Ads upload-ready CSV. A related Figma plugin takes headline variations and a selected creative frame to generate creative permutations. The reusable context and review process matter alongside the automation. [Anthropic’s marketing workflow](https://claude.com/resources/articles/how-anthropic-uses-claude-marketing).

**Inbound qualification at Anthropic.** A small GTM team needed to qualify a large volume of interest despite incomplete data and manual Salesforce work. Clay’s customer account describes enrichment across providers, Claude-based industry classification, lead scoring, and matching personal signups to work identities. The output is enriched, standardized Salesforce records that support prioritization, with conditional opportunity and account updates. This is a vendor-reported company implementation. [Anthropic’s Clay implementation](https://www.clay.com/customers/anthropic).

**Signal-based sales at Vanta and Amplitude.** The problem is recognizing relevant account changes and opportunities. Clay reports that Vanta monitors SOC 2 announcements, compliance-related website changes, funding, and CISO job postings. Amplitude combines its product data with AI research to identify customers suited to cross-sell. The useful output is account context for prioritization and follow-up. These examples illustrate the broader pattern of inputs, interpretation, and actionable output; the source does not establish repository-based implementations. [Clay’s signal examples](https://www.clay.com/signals).

**A literal folder-based workspace.** Databar’s implementation guide addresses scattered GTM context with a proposed workspace containing ideal customer profile (ICP), positioning, voice, account notes, procedures, campaign materials, and CSV inputs and outputs. Reusable instructions and live data access support tasks such as account briefs and pipeline reviews, with results kept alongside campaign work. It is a setup guide, not evidence of a named company’s production results, and it also includes optional subagents and memory tooling. [Databar’s workspace guide](https://databar.ai/blog/article/claude-code-as-your-gtm-second-brain).

These sources illustrate useful workflow patterns. They do not prove that agents are unnecessary or that a repository-based approach always performs better. I’m exploring this approach for GTM work and will add my own implementations and evidence over time.
