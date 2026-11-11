# “Can wait” tagging re-evaluation: November 10, 2026

**Measured result.** router-v1.9 passed the two evaluation sets under the revised label rules: none of the 114 emails routed to no action on gate1-v1 needed action, and all 19 regression cases routed correctly. I activated v1.9 that evening, replacing v1.7. This is backtest evidence, not a measured live v1.9 miss rate.

**Source and scope.** This note summarizes my evaluation record from November 10, 2026, including n8n backtest results and my review labels. Customer examples are sanitized paraphrases; names, message identifiers, and verbatim email text are omitted. The reported counts are unchanged.

## Why I ran it

Advisory tagging went live with production traffic on November 10 using router-v1.7, whose classification was unchanged from v1.5. A customer’s confirmation of a call received a “Can wait” tag, prompting me to inspect the configuration. Its no-request intent included call setup, attachments sent for us to use, and follow-up nudges as examples needing no action.

The triggering call example was initially treated as a miss. After reviewing the thread, I changed its label to “could wait”: the rep had already proposed a time and the customer was confirming it. It is not a confirmed miss under the final rules.

A keyword check of the first 243 live v1.7 no-action decisions found 5 mentioning calls, 4 mentioning attachments, and 8 resembling follow-ups. These are keyword matches, not confirmed misses or a measured error rate.

## Samples and method

| Set | Contents | Purpose |
| --- | --- | --- |
| gate1-v1 | The 275 scored emails from the original 300-email gate sample | Recheck tagging against the original sample with revised labels |
| noaction-regression-v1 | 19 emails drawn from reviewed live misses and sign-off controls | Check specific problem cases and emails that should still receive the tag |

I was the sole reviewer, labeling whether each email needed action or could wait. A tagging miss is an email labeled “needed action” that the router sends to no_action, which applies the Front tag. The tagging gate uses a bar of about 2% misses among no-action predictions. For this re-evaluation, I required zero labeled misses on gate1-v1 and correct routing on every regression row.

I set two label rules during the review:

- All approvals need action, including short acknowledgments of approval. Five gate1-v1 emails previously labeled “could wait” or “not sure” were relabeled “needed action.”
- A confirmation of a call the rep already booked can wait. This changed the label of the triggering production example.

## Changes and results

router-v1.8 narrowed no-request wording to true sign-offs and treated call requests, files sent for us to use, and follow-ups as needing action. Its gate1-v1 run exposed short approvals still being routed to no action. I added an explicit approvals rule in v1.9.

| Run | Coverage | Recorded outcome |
| --- | --- | --- |
| v1.8, November 10 | gate1-v1 only; a set-ID mistake omitted the regression set | Exposed approval errors; no full result count is included in the supplied record |
| v1.9, November 10 | Both sets; 290 unique emails, no run errors | 0 of 114 tagged gate1-v1 emails needed action; all 19 regression cases routed correctly |

The sets overlap, so 275 plus 19 does not represent 294 unique test emails. Regression correctness and the gate1-v1 tagging miss rate use different denominators and are reported separately.

v1.9 tagged 114 gate1-v1 emails, compared with 121 in the original v1.5 run. The evaluation record describes the cases it stopped tagging as conservative decisions to send work to a person. This reduction in tagging is a tradeoff, not evidence of improved overall routing accuracy. Any comparison that rescores v1.5 under the new labels is a retrospective relabeling of the original run, not a new v1.5 run.

## Limitations

- **Used in tuning.** gate1-v1 informed the approvals fix, and the live examples informed v1.8 wording. Neither set is a clean holdout for v1.9.
- **Small samples.** Zero misses among 114 tagged emails does not establish a zero miss rate. The supplied evaluation reports an approximate 95% upper bound of 3.2%, still above the 2% gate bar.
- **One reviewer and changing labels.** I set two rules during the evaluation and applied them retroactively.
- **Narrow regression coverage.** The regression set came from one day of traffic and keyword-led review. Neither set contains a request for a call that has not already been booked.
- **Only part of the workflow measured.** The gate checks whether tagged emails needed action. It does not establish how many eligible emails were left untagged or measure overall intent and handoff quality.
- **No live v1.9 result yet.** At the time of the evaluation record, v1.9 had been activated but not yet observed on production traffic.

## Decisions and next checks

I activated v1.9 on the evening of November 10. The recorded rollback option was to reactivate v1.7, whose wording prompted this review.

Every future configuration version must pass gate1-v1 and noaction-regression-v1. I will add confirmed live no-action misses to the regression set, spot-check live v1.9 tags, and add the first real unbooked call request when one is available. These sets check known cases; fresh production review is still needed.

## Comparison with the original gate

| | Original gate | Re-evaluation |
| --- | --- | --- |
| Date | November 6, 2026 | November 10, 2026 |
| Purpose | Decide whether to enable advisory tagging | Investigate production observations and check revised configuration |
| Configuration | router-v1.5 | router-v1.8 and router-v1.9 |
| Sample | 300 sampled, 275 scored; 121 no-action predictions reviewed | The same 275 scored emails plus a 19-email regression set; 290 unique emails in the v1.9 run |
| Labels | Rules used on November 6 | Revised approval and booked-call rules |
| Result | 1 of 121 tagged emails needed action (0.8%); passed | v1.9: 0 of 114 on gate1-v1; all 19 regression cases correct; passed |

The results are not combined because the label rules changed and the samples overlap. See the [original evaluation methods and limitations](source-notes.md#gate-1--advisory-can-wait-tagging).

[Back to evaluation index](README.md) · [Back to case study](../README.md)
