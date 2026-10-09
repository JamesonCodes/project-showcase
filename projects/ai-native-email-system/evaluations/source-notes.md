# AI Native Email System source notes and evidence gaps

This documentation draft was adapted on October 9, 2026 from the local portfolio repository at revision `0021813abcdf870b8e0b777f0e3b6166d38c62d7`. The source article displays August 27, 2026 as its publication date; this is not the project's start or launch date. No application source, Front messages, Supabase rows, or production dataset was inspected.

## Sources

- [Build journal at the inspected revision](https://github.com/JamesonCodes/JamesonCodes.github.io/blob/0021813abcdf870b8e0b777f0e3b6166d38c62d7/articles/ai-native-email-system.html): architecture, live-versus-planned scope, human review, reported observations, projections, and next evaluation work.
- [Project cards at the inspected revision](https://github.com/JamesonCodes/JamesonCodes.github.io/blob/0021813abcdf870b8e0b777f0e3b6166d38c62d7/index.html): system and plugin tools.
- [Published build journal](https://jamesoncodes.github.io/articles/ai-native-email-system.html): reader-facing account; later changes may differ from this snapshot.

## Evidence classification

| Claim | Source characterization | What is missing |
| --- | --- | --- |
| 500+ submissions | Observed volume since launch | Launch date, reporting end date, denominator, and export |
| ~24-second median | Measured submission time in article | Timing start/end definitions, sample, and export |
| Roughly 3–4 minutes manually | Approximate baseline | Measurement method and baseline period |
| ~1 in 5 second full design cycles | Rework observation | Denominator, period, definition, and comparable baseline |
| ~0.6–0.7 FTE Sales Support capacity | Annualized projection | Expected volume, working-hours assumption, and calculation |
| 168 hours / ~1% design capacity | Annualized projection | Calculation, expected volume, and relationship to rework |
| First 80% of useful routing taxonomy | Informal qualitative judgment | Not an accuracy score; use a labeled evaluation set instead |

The rough baseline and reported median support the article's approximate time-reduction claim, but they do not establish an independently verified controlled before/after study. Capacity is conditional and does not imply staffing reductions. No claimed improvement in design rework can be inferred without its baseline.

## Evaluation work described as in progress

The journal proposes separate datasets for the action/no-action gate, action categories, and no-action categories. Senior teammates will label examples drawn from logs, enabling repeatable model and prompt comparisons. Do not mark these datasets complete or invent accuracy thresholds.

{Add sanitized reviewed examples, label definitions, dataset size, measurement period, model/prompt versions, scores, and inspected failure cases}

The article labels its jobs repository and autonomy matrix as sanitized working views. The diagram is a conceptual illustration, not a production execution trace. Any new inbox example must be explicitly labeled real, sanitized, or synthetic.
