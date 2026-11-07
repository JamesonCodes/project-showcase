# AI-Native Sales Email System evidence notes

The case study uses the updated architecture diagram to distinguish live intake and enrichment, shadow routing, and downstream work in development or planned.

## First routing review

- **Sample.** 50 recent inbound emails, one per conversation, with 40 to 1,500 characters per message. Automated sequence messages and messages previously routed or replayed were excluded.
- **Selection.** The sample was stratified across ten work-area buckets from the earlier capacity study. Those buckets served as a sampling proxy. Overlap with the intent discovery corpus was not verified.
- **Review.** A person checked whether action was needed and reviewed the primary and secondary intents. They judged 39 decisions right, 5 wrong, and 6 uncertain. Of the 44 definite judgments, 5 were wrong (11.4%), above the 5% job promotion threshold.
- **Replay finding.** In a separate impact check of about 135 replayed rows and 45 logged decisions, the complaint in the walkthrough was the only reported problem routed to no action. The same message routed to a person in later replays under v1.3, v1.4, and v1.5. The configuration changed between runs, and this case informed the fix. Its replays show how the revised router handles the example.

## Current evidence gaps

The broader historical backtest and comparison against rep actions remain planned. A fresh sample is needed to assess the complaint rule on unseen mail. End-to-end job completion and production outcomes remain undocumented.

## Historical background

The original draft was adapted on October 9, 2026 from the portfolio repository at revision `0021813abcdf870b8e0b777f0e3b6166d38c62d7`.

- [Earlier build journal at the inspected revision](https://github.com/JamesonCodes/JamesonCodes.github.io/blob/0021813abcdf870b8e0b777f0e3b6166d38c62d7/articles/ai-native-email-system.html), published August 27, 2026: historical context for the shared pipeline, category-routing discovery loop, and autonomy framework. It does not establish the project's current implementation or next steps.

The pipeline diagram is conceptual, not a production execution trace. Label new examples real, sanitized, or synthetic and remove confidential information.
