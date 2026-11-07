# AI-Native Sales Email System evidence notes

The case study uses the updated architecture diagram to distinguish live intake and enrichment, shadow routing, and downstream work in development or planned.

## Gate 1 — Advisory no-action tagging

- **Scope.** v1.5 could pass the gate if at most 2% of emails it marked no action actually needed action. The gate record containing the threshold was created after labeling. Whether the threshold was set beforehand is unverified.
- **Sample.** 300 random inbound emails over roughly seven weeks, one per conversation. The sample excluded automated sequences, bodies outside 2 to 3,000 characters, and messages or conversations used in prior runs or logged decisions. It retained auto-replies and short replies. Overlap with the intent discovery corpus is unknown.
- **Review.** The router scored 275 and skipped 25 without errors. The reported empty-body explanation conflicts with nonblank cleaned text in the logs. Skipped messages cannot receive the tag. A single reviewer saw the router output and the same thread context, with rep replies hidden. They labeled only the 121 predicted no-action messages.
- **Result.** One of 121 needed action (0.8%, approximate 95% interval of 0.1% to 4.5%). The point estimate passed. The other 154 scored messages were unlabeled, so the gate leaves action recall, intent quality, and handoff quality unmeasured.
- **Deployment.** The active configuration enables tagging and one end-to-end test applied the tag. Reproduction of the gated decisions under the active configuration is unverified. No production traffic calls the router yet. The tag-removal rule is built and remains disabled.

## Exploratory intent and routing review

- **Sample.** 50 recent inbound emails, one per conversation, with 40 to 1,500 characters per message. Selection spanned ten work-area buckets from an earlier capacity study. Those labels served as a sampling proxy. The sampling method within each bucket and overlap with intent discovery are unknown. One conversation overlapped an earlier tuning set. The 50 messages were held out of v1.1 and v1.2 tuning and informed v1.3 through v1.5. The 300-email gate sample has no message or conversation overlap with this review.
- **Review.** One reviewer saw the router output and up to three prior thread messages, with rep replies hidden. They gave one overall judgment covering needs-action, primary and secondary intents, job, and route. Secondary-intent criteria were written after labeling and applied inconsistently. No field-level scores are available.
- **Result.** The initial review recorded 3 wrong out of 39 definite judgments (7.7%). After teammate input resolved five uncertain cases, the totals were 39 right, 5 wrong, and 6 uncertain. The resulting error rate was 11.4% (5 of 44 definite judgments). The dropped complaint remained uncertain and is excluded. The working bar of about 5% wrong with no high-stakes misses applies per job. The pooled review had no formal pass or fail.
- **Iteration.** Three of the five wrong decisions confused date, shipping, status, or sample requests. v1.5 reduced the count to 3 wrong out of 44 on the same cases used to tune it. A new labeled sample is needed to measure intent quality on fresh mail, ideally with a second reviewer on a subset.

## Historical background

The original draft was adapted on October 9, 2026 from the portfolio repository at revision `0021813abcdf870b8e0b777f0e3b6166d38c62d7`.

- [Earlier build journal at the inspected revision](https://github.com/JamesonCodes/JamesonCodes.github.io/blob/0021813abcdf870b8e0b777f0e3b6166d38c62d7/articles/ai-native-email-system.html), published August 27, 2026: historical context for the shared pipeline, category-routing discovery loop, and autonomy framework. It does not establish the project's current implementation or next steps.

The pipeline diagram is conceptual, not a production execution trace. Label new examples real, sanitized, or synthetic and remove confidential information.
