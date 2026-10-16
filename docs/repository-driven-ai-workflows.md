# Repository-driven AI workflows

*An exploration of repeatable GTM work.*

“Repository-driven AI workflows” is my descriptive label for keeping work materials together. A project folder holds context, reusable instructions, plans, scripts, inputs, outputs, QA records, logs, and lessons. The goal is repeatable, inspectable AI-assisted work without rebuilding context every conversation. This is not a standardized framework.

## Start with the simplest reliable system

> Building a custom agent is often the wrong starting point. Before investing in orchestration, memory systems, and autonomous loops, see whether clear instructions, persistent files, scripts, and API access solve the problem. Build the simplest system that reliably gets the work done.

Unnecessary infrastructure consumes time and maintenance effort. An existing coding assistant may already supply file access, tools, scripts, and multi-step execution. Custom agents remain useful when requirements exceed those capabilities.

## Make the work reusable

The value is the working process, not the folders themselves. Start with a task, define acceptable output and review points, preserve inputs, and record corrections. Scripts handle repeatable transformations; APIs supply current information or execute approved actions.

Keep useful records alongside the work:

- **Plans:** Markdown files with goals, decisions, status, and next steps.
- **QA notes:** Checks, failures, and unresolved issues.
- **Run logs:** Dated inputs, commands, outputs, and fixes so future agents can resume work without repeating failed approaches.

Keep records current, distinguish planned from completed work, and remove secrets before committing logs.

## Related approaches

Jake Van Clief and David McDermott’s **Interpretable Context Methodology (ICM)** provides a closely related architectural reference: staged folders, explicit inputs and outputs, selective context loading, and separate reusable guidance and working artifacts. It still uses agents while reducing custom orchestration. Their paper reports preliminary practitioner experience, not controlled evidence of superior performance. [ICM paper](https://arxiv.org/html/2603.16021v2), [implementation repository](https://github.com/RinDig/Interpretable-Context-Methodology).

Vercel’s **Eve** extends a directory-based approach into deployed agents: Markdown instructions and skills sit alongside TypeScript tools, with a framework providing durable execution and integrations. I see this as a possible next step when requirements justify infrastructure beyond an existing assistant. [Vercel Eve](https://vercel.com/eve).

## Examples in GTM

These external examples are other teams’ work, not my implementations.

### Ad production at Anthropic

Producing fresh ads involved repeated copy creation, character checks, and movement between tools. Anthropic describes a Claude Code workflow that combines campaign performance data, existing copy, and keywords with reusable brand, product, and advertising instructions. A marketer refines and reviews the copy before export to a Google Ads upload-ready CSV. A related Figma plugin takes headline variations and a selected creative frame to generate creative permutations. [Anthropic’s marketing workflow](https://claude.com/resources/articles/how-anthropic-uses-claude-marketing).

### A literal folder-based workspace

Databar’s implementation guide addresses scattered GTM context with a proposed workspace containing ideal customer profile (ICP), positioning, voice, account notes, procedures, campaign materials, and CSV inputs and outputs. Reusable instructions and live data access support tasks such as account briefs and pipeline reviews, with results kept alongside campaign work. It is a setup guide, not evidence of a named company’s production results, and it also includes optional subagents and memory tooling. [Databar’s workspace guide](https://databar.ai/blog/article/claude-code-as-your-gtm-second-brain).

## Potential application: client service delivery

I see this approach fitting AI-native service businesses that deliver repeatable work for clients. Shared procedures and QA standards can guide delivery, while each client’s workspace holds their context, plans, inputs, deliverables, approvals, and lessons. The opportunity is a repeatable process with client-specific judgment and a clear record of the work. This is an application I’m exploring, not a validated business model.

## What I’m exploring next

These sources illustrate useful workflow patterns. They do not prove that agents are unnecessary or that a repository-based approach always performs better. I’m exploring this approach for GTM work and will add my own implementations and evidence over time.
