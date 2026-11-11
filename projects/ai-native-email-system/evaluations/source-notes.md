# AI-Native Sales Email System evidence notes

The tagging gate measures how often a “can wait” prediction misses work. The intent review examines the router’s broader decisions about what the customer needs and who should handle it.

## Review workflow

I’m still learning how to design good evaluations. These first reviews gave me a way to inspect decisions, document misses, and see where the method itself needs work.

I built a Claude artifact to guide reviewers through email examples and routing decisions. It made the review easier to work through and gave me something I could share internally to guide teammates through the same process.

## Gate 1 — Advisory “can wait” tagging

**Decision.** Can the router apply an advisory “can wait” tag to emails it predicts need no action? The gate allows up to 2% of those predictions to be misses. The denominator is the set of emails predicted to need no action. The stored gate record was created after labeling, and whether the threshold was set beforehand is unverified.

**Sample and review.** I randomly selected 300 inbound emails over roughly seven weeks, one per conversation. I excluded outbound email, automated sequences, bodies outside 2 to 3,000 characters, and messages or conversations used in earlier runs or logged decisions. Auto-replies and short replies stayed in the sample. There was no overlap with the 50-message intent review at either the message or conversation level. Overlap with the intent discovery corpus is unknown.

The router ran v1.5. A single reviewer saw the newest message, the same earlier thread messages the router saw, and the router output. The rep’s actual reply was hidden. The reviewer answered “could this wait?” for each predicted no-action email.

| Measure | Count or result |
| --- | --- |
| Emails sampled | 300 |
| Emails scored | 275 |
| Emails skipped | 25 |
| Run errors | 0 |
| Predicted no action and reviewed | 121 |
| Scored but unlabeled | 154 |
| Reviewed emails that needed action | 1 |
| Miss rate among predicted no-action emails | **0.8% (1 of 121)** |
| Approximate 95% interval | 0.1% to 4.5% |
| Gate outcome | **Passed** on the point estimate against the 2% bar |

Skipped messages cannot receive the tag. The run reported empty bodies for those 25 skips, but the message log shows nonblank cleaned text. The reason is unverified. The 154 other scored emails were deliberately left unlabeled, so action recall, intent quality, and handoff quality remain unmeasured by this gate.

**The miss.** A short reply said a logo was attached. With no earlier thread messages available, the router scored needs-action at 0.07 and identified a possible new project with 0.40 confidence. It chose no action. The email needed a new project and design request. Two candidate rules would have caught the miss in this sample:

| Candidate rule for predicted no-action emails | Would route to a person |
| --- | --- |
| Route decisions with intent confidence under 0.65 | 40 of 121 (33%) |
| Route decisions with an action intent | 12 of 121 (about 10%) |

Both rules remain proposals.

**Rollout history.** Advisory tagging went live with production traffic on November 10, 2026 using v1.7, whose classification was unchanged from v1.5. Production observations prompted a separate re-evaluation, revised label rules, and activation of v1.9 that evening. The original result above retains its November 6 labels. See the [November 10 re-evaluation](can-wait-reevaluation-2026-11-10.md) for the later results and live follow-up plan. An earlier record described tag removal on new messages as built but disabled; its current status is not established by the re-evaluation.

## Exploratory intent and routing review

**Decision.** This review examined whether v1.2 could identify the work in an email and recommend an appropriate handoff. The working promotion bar was about 5% wrong with no high-stakes misses, applied per job. The review pooled decisions across 14 intents, with too few examples for per-job rates. No formal gate outcome was recorded.

**Sample and review.** I selected 50 recent inbound messages from a two-week window, one per conversation. I excluded automated sequences, bodies outside 40 to 1,500 characters, previously routed or replayed messages, and obvious auto-replies. One out-of-office reply slipped through and was kept. The sample spans ten work-area buckets from an earlier capacity study. The AI-assigned bucket labels helped spread the sample and were never scored. The selection method within each bucket and overlap with the intent discovery corpus are unknown.

The messages were held out of v1.1 and v1.2 tuning. One conversation overlapped an earlier tuning set, and these 50 cases later informed v1.3 through v1.5. One reviewer saw the newest email, up to three earlier messages, and the router output. The rep’s reply was hidden. The reviewer gave one verdict covering needs-action, primary and secondary intents, job, and route. Secondary-intent criteria were written after labeling and applied inconsistently. The record supports overall verdicts only.

| Review stage | Right | Wrong | Uncertain | Error rate among definite judgments |
| --- | ---: | ---: | ---: | ---: |
| Initial v1.2 review | 36 | 3 | 11 | 7.7% (3 of 39) |
| v1.2 after teammate input on five uncertain cases | 39 | 5 | 6 | **11.4% (5 of 44)** |

Three of the five wrong decisions confused date, shipping, status, or sample requests. Two went to an agent route. The [dropped product complaint](../README.md#a-routing-decision-from-a-historical-replay) remained uncertain and falls outside the error rate.

| Version | What the replay showed |
| --- | --- |
| v1.3 | Clarifying the date, shipping, status, and sample categories fixed those primary intents and broke three secondary intents. |
| v1.4 | A broader secondary-intent rule fixed two rows and introduced other errors. The needs-action score also shifted sharply across versions on one short reply. |
| v1.5 | Narrower notes gave the best result on these same cases, with 3 of 44 definite judgments wrong (6.8%). The cases informed the tuning, so this is an in-sample result. |

**Next test.** Run a fresh intent review and have a second person label a subset. The 300-email tagging sample had no intent labels, so fresh intent accuracy remains unmeasured. The revised complaint rule needs examples that did not inform the fix.

## Historical background

The original draft was adapted on October 9, 2026 from the portfolio repository at revision `0021813abcdf870b8e0b777f0e3b6166d38c62d7`.

- [Earlier build journal at the inspected revision](https://github.com/JamesonCodes/JamesonCodes.github.io/blob/0021813abcdf870b8e0b777f0e3b6166d38c62d7/articles/ai-native-email-system.html), published August 27, 2026: historical context for the shared pipeline, category-routing discovery loop, and autonomy framework. It does not establish the project's current implementation or next steps.

The pipeline diagram is conceptual, not a production execution trace. Label new examples real, sanitized, or synthetic and remove confidential information.
