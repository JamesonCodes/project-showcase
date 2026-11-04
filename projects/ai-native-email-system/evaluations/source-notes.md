# AI Native Email System source notes and evidence gaps

This documentation draft was adapted on October 9, 2026 from the local portfolio repository at revision `0021813abcdf870b8e0b777f0e3b6166d38c62d7`. The source article displays August 27, 2026 as its publication date; this is not the project's start or launch date. No application source, Front messages, Supabase rows, or production dataset was inspected.

## Sources

- [Build journal at the inspected revision](https://github.com/JamesonCodes/JamesonCodes.github.io/blob/0021813abcdf870b8e0b777f0e3b6166d38c62d7/articles/ai-native-email-system.html): architecture, live-versus-planned scope, human review, reported observations, projections, and next evaluation work.
- [Published build journal](https://jamesoncodes.github.io/articles/ai-native-email-system.html): reader-facing account; later changes may differ from this snapshot.

## Evidence scope

This case study covers shared context, category routing, job definition, and earned autonomy. Workflow-specific submission metrics and capacity projections are outside its scope.

- **Source-reported process observation:** The shadow router logs real conversations for batch analysis and iterative refinement. No production export has been inspected here.
- **Intended architecture:** Job identification, policy decisions, execution, and outcome evaluation describe the downstream system design, not verified end-to-end implementation.
- **Unmeasured outcomes:** Router accuracy, end-to-end job completion, and system-wide time savings are not established by the available evidence. The journal's informal taxonomy-coverage assessment is not an accuracy score.

## Evaluation work described as in progress

The journal proposes separate datasets for the action/no-action gate, action categories, and no-action categories. Senior teammates will label examples drawn from logs, enabling repeatable model and prompt comparisons. Do not mark these datasets complete or invent accuracy thresholds.

{Add sanitized reviewed examples, label definitions, dataset size, measurement period, model/prompt versions, scores, and inspected failure cases}

The article labels its jobs repository and autonomy matrix as sanitized working views. The diagram is a conceptual illustration, not a production execution trace. Any new inbox example must be explicitly labeled real, sanitized, or synthetic.
