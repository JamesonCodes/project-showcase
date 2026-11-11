# “Can wait” tagging follow-up: November 10, 2026

**Result:** v1.9 passed the follow-up tests. None of the 114 tagged emails in the original test set needed action, and all 19 regression cases routed correctly. I activated v1.9 that evening, replacing v1.7. These are backtest results; live v1.9 performance had not yet been reviewed.

This note summarizes my evaluation record and n8n backtests. Customer examples below are sanitized paraphrases, with names and message identifiers omitted.

## What prompted the review

Tagging went live on November 10 with v1.7, which classified emails the same way as v1.5. A tagged call confirmation led me to inspect the configuration. It treated call setup, attachments, and follow-up nudges as examples needing no action.

After reading the thread, I decided that particular confirmation could wait: the rep had already booked the call. It was not a confirmed miss under the final review rules, but it exposed wording worth fixing.

A keyword check of the first 243 live no-action decisions found 5 mentioning calls, 4 mentioning attachments, and 8 resembling follow-ups. Those matches were leads for review, not confirmed errors.

## What I changed and tested

v1.8 narrowed the no-action category to true sign-offs. Call requests, files sent for us to use, and follow-ups now counted as needing action. Testing then exposed short approvals being tagged, so v1.9 added an explicit rule: all approvals need action.

I also clarified that a confirmation of an already booked call can wait. Under these rules, I relabeled five emails in the original set as needing action and the triggering call example as able to wait.

| Test set | Contents | v1.9 result |
| --- | --- | --- |
| Original set (`gate1-v1`) | 275 scored emails from the original 300-email sample | 0 of 114 tagged emails needed action |
| Regression set (`noaction-regression-v1`) | 19 cases drawn from reviewed live misses and sign-offs | All 19 routed correctly |

The sets overlap: the combined run covered 290 unique emails with no run errors. I was the only reviewer. To pass this follow-up, I required no tagging misses in the original set and correct routing on every regression case. The general tagging gate allows about 2% misses among tagged emails.

The v1.8 run accidentally omitted the regression set because of a set-ID mistake. The v1.9 run covered both sets.

v1.9 tagged fewer emails: 114 versus 121 in the original v1.5 run. The record describes the cases it stopped tagging as conservative handoffs to a person. This test does not measure overall routing accuracy.

## What the result does and does not establish

- **The examples helped shape the fix.** Both sets were used during tuning, so a fresh review is still needed.
- **The sample is small.** Zero misses out of 114 gives an approximate 95% upper bound of 3.2%, above the 2% gate bar.
- **The labels changed.** I was the sole reviewer and applied the new approval and booked-call rules retroactively.
- **Coverage is limited.** The regression cases came from one day of traffic and keyword-led review. Neither set tests a call request where no call is booked yet.
- **The gate checks tagged emails.** It does not measure how many other emails could safely have received the tag, or the quality of agent handoffs.

## Next steps

Every future configuration must pass both sets. I’ll add confirmed live misses to the regression set, spot-check live v1.9 tags, and add a real unbooked call request when one is available. The recorded rollback option was v1.7.

## Keep the original result separate

The [November 6 gate](source-notes.md#gate-1--advisory-can-wait-tagging) used v1.5 and found 1 miss among 121 tagged emails (0.8%), with an approximate 95% interval of 0.1% to 4.5%. It passed under the review rules used at the time.

This follow-up reused that sample with revised labels and added regression cases. The results are not combined. Rescoring the old v1.5 output with new labels is a retrospective comparison, not a new run.

[Back to evaluation index](README.md) · [Back to case study](../README.md)
