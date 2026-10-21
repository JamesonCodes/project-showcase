# Decision Council

A structured prompt for examining a decision through five perspectives, challenging assumptions, and choosing practical next steps. I’m collecting this as a decision aid to test, not a proven way to remove AI bias.

**Status:** Exploratory; no evaluated example run is documented here.

## How to use

Copy the prompt into an AI chat. It first asks about the decision and waits for your answers, then produces five perspectives, a critique, and a recommendation. Share relevant evidence and constraints; remove confidential information before using an external service.

The five voices are simulated perspectives from one assistant. They are not independent advisers, separate models, or anonymous reviewers. Use their arguments to identify questions to investigate, not as five independent confirmations.

## Supporting context and attribution

- **Why challenge agreement:** Stanford researchers evaluated 11 models on advice tasks. In the general-advice and Reddit-based prompts, models affirmed users’ positions 49% more often than humans on average. This is a relative comparison across the tested models and prompts, not a Claude-specific result or a claim about every kind of advice. [Stanford research summary](https://news.stanford.edu/stories/2026/03/ai-advice-sycophantic-models-research), [paper DOI](https://doi.org/10.1126/science.aec8352).
- **Why a council structure:** Andrej Karpathy’s [LLM Council](https://github.com/karpathy/llm-council) collects responses from multiple models, asks them to review and rank anonymized responses, and synthesizes an answer. This prompt borrows that broad sequence within a single chat; it does not reproduce the implementation or establish equivalent results.
- **What remains untested:** These sources motivate scrutiny and provide a design reference. They do not validate this prompt as a remedy for sycophancy or demonstrate better decisions. Role labels, disagreement, and confident language are not evidence of accuracy.

Adapted with AI assistance from a council prompt supplied to me. The original author of that wording was not identified in the supplied material; I do not attribute the five-role prompt to Karpathy. I removed the supplied claims that one prompt fixes sycophancy and that Karpathy works at Anthropic, and replaced simulated anonymity with an explicit critique step.

## Copy the prompt

```text
Run a structured decision review using five simulated adviser perspectives. Help me examine the evidence rather than echo my preference. Agreement and disagreement must both be justified; do not flatter me or manufacture objections.

These are perspectives generated within one chat, not independent advisers or anonymous peer review. Do not claim to have consulted other models, people, or sources unless you actually have.

Step 0: Interview me first

Ask the following in ONE message, then stop and wait for my answers. Ask only for information I have not already provided:
1. What is the decision? Name the specific options, including waiting or doing nothing where relevant.
2. What is the context? Include money, time, people, relevant evidence, and what I have tried.
3. What would a good outcome look like in 12 months, or another relevant time frame?
4. What are my constraints and non-negotiables?
5. When must I decide, and what does waiting cost?
6. Which option am I leaning toward, and why?
7. What am I most afraid of?

If needed, ask up to two short follow-up questions before proceeding. Restate the decision in two sentences, distinguishing known facts from assumptions.

Step 1: Five perspectives

Write five labeled sections of about 100–180 words each. Apply each perspective separately before comparing them. Do not treat my preference as the default or claim the sections were generated independently.

1. THE CONTRARIAN: Focus on failure. Name the likeliest failure mode, what breaks first, the worst realistic outcome, and an early warning sign. Distinguish plausible risks from speculative ones.
2. THE FIRST-PRINCIPLES THINKER: List 3–5 assumptions. Mark each supported, plausible, or untested and explain the evidence or gap. Ask whether starting from zero would lead to the same choice.
3. THE EXPANSIONIST: Explore overlooked upside and an Option C that might improve the tradeoff. Explain its costs and requirements without assuming the upside will happen.
4. THE OUTSIDER: Use plain language. Pose three questions a thoughtful newcomer would ask, and identify anything insiders may take for granted. Do not invent answers to missing facts.
5. THE EXECUTOR: Identify concrete first moves and the cheapest useful test that could reduce uncertainty within two weeks. State what the test can and cannot establish.

Step 2: Critique the arguments

This is a structured self-critique, not a blind review. Keep adviser labels visible. For each perspective, briefly identify:
- Its strongest supported point.
- Its biggest unsupported assumption, error, or omission.
- What evidence would strengthen or weaken it.

Then identify the most important disagreement. Explain whether it comes from conflicting facts, assumptions, values, or risk tolerance. Do not force consensus or count repeated claims as independent evidence.

Step 3: Chair's recommendation

Use the following format and stay under 350 words:
- THE CALL: Recommend an option when the evidence supports one. If a missing fact could reverse the decision, give a conditional recommendation and explain how to obtain that fact. Prefer a reversible test or waiting when justified; do not manufacture certainty.
- CONFIDENCE: Low, Medium, or High, with the main uncertainty and what would change the recommendation. This is a qualitative assessment, not a calibrated probability.
- WHY: The 2–3 strongest reasons, tied to evidence or clearly labeled assumptions.
- BIGGEST RISK: The risk and a practical way to limit it.
- WHERE THE PERSPECTIVES SPLIT: The sharpest disagreement and why one argument carries more weight.
- WHERE I MIGHT BE FOOLING MYSELF: Compare the recommendation with my stated preference. If they match, identify support beyond my wanting that result.
- NEXT STEPS: 3–5 actions with realistic deadlines relative to my decision date. The first should take under an hour. Do not send messages or take external actions.
- RECONSIDER IF: Observable signals in a relevant time frame that should trigger review or reversal.

Rules throughout

- Separate user-reported facts, verified evidence, assumptions, and unknowns. Never invent facts, statistics, sources, or details about my situation.
- If you can research current or disputed facts, use reliable primary sources and cite them. Otherwise state what needs verification; do not imply research occurred.
- Challenge the framing as well as the options. Consider who else is affected and whether their interests are missing.
- When I push back, reassess the reasoning. Change the recommendation when evidence, corrected reasoning, or clarified priorities justify it, and explain what changed.
- For legal, medical, tax, or major financial decisions, identify what requires qualified professional input. Do not force a definitive call beyond the available evidence or your competence.
- After the recommendation, offer one optional follow-up: a pre-mortem, a stress test, or a rerun with one assumption changed.
```

[Back to the prompt directory](README.md)
