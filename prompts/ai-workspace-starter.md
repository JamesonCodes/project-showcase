# AI Workspace Starter

A starting prompt for setting up a small, folder-based AI workspace for repeatable work. The assistant asks about the workflow, proposes a structure, and creates it locally after agreement.

**Status:** Exploratory; no evaluated example run is documented here.

This is a practical adaptation inspired by Jake Van Clief and David McDermott’s [Interpretable Context Methodology (ICM)](https://github.com/RinDig/Interpretable-Context-Methodology), not an official template.

## How to use

Copy the prompt below into your coding assistant. Be ready to describe the work you want to repeat, available inputs, expected output, and where human review matters. Adapt the proposed structure to your needs.

```text
Help me set up a folder-based AI workspace inspired by Jake Van Clief and David McDermott’s Interpretable Context Methodology (ICM):
https://github.com/RinDig/Interpretable-Context-Methodology

First, ask me what workflow I want to repeat, what inputs I have, what deliverable I need, and where human review matters. Ask only what you need to propose a useful first version.

Then:
1. Propose the simplest folder structure that fits the workflow. Explain each folder’s purpose.
2. Separate reusable guidance, such as brand voice and quality standards, from inputs and outputs specific to each run.
3. Break the workflow into numbered stages where useful. Give each stage Markdown instructions defining its inputs, process, outputs, and review checkpoint.
4. Create a short root instruction file that maps the workspace and tells the assistant which files to read for each task. Avoid loading everything at once.
5. Include places for Markdown plans, QA findings, and dated run logs so future sessions can understand decisions, completed work, failures, and next steps.
6. Use scripts for mechanical steps when useful. Identify required API access without inventing integrations or storing credentials.
7. Walk through one example run and check that each stage produces what the next stage needs.

Keep the structure small. Do not create empty folders, unnecessary agents, or orchestration infrastructure. Mark missing information clearly and distinguish planned work from completed work.

Create the workspace locally after we agree on the structure. Do not send messages, publish outputs, modify external systems, commit, or push without my approval.

Treat this as a practical adaptation inspired by ICM, not an official implementation or a guarantee of better results.
```

## Related material

- [Repository-driven AI workflows](../docs/repository-driven-ai-workflows.md)
- [Prompt directory](README.md)
