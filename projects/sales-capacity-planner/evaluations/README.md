# Evaluations

[Back to the case study](../README.md)

These evaluations used **real internal email data**. Raw messages, manual reference labels, and customer communications remain private.

## Find an evaluation

| Evaluation | Scope | What it checks |
| --- | --- | --- |
| [Prompt comparisons](#classifier-prompt-comparisons) | 156 manually labelled messages | Matching labels and category proportions |
| [Backfill audit](#full-backfill-audit) | 40 sampled records from 3,579 messages | Agreement with an AI reviewer and consistent labelling |
| [How distinct are the categories?](#how-distinct-are-the-categories) | 420 labelled messages | How much category text overlaps |
| [Grouping emails without preset categories](#grouping-emails-without-preset-categories) | 1,985 emails after removing duplicates | Exploring how emails group into types |
| [Checking snapshot totals](#checking-snapshot-totals) | 13,117 messages | Whether records are accounted for |

These checks do not measure business impact or confirm that estimated hours are accurate. Sources are my internal prompt documentation, historical classification audit, embedding analyses, and snapshot notes.

## Classifier prompt comparisons

- **Reference:** One account manager's manually labelled time-study log, updated to use the current six categories.
- **Sample:** 156 messages with both a manual label and an AI label.
- **Reviewed:** September 22–23, 2026, by reviewing messages directly. The test did not run through the full automated process.

### Results

| Prompt version | Agreement | Category mix error | Main change |
| --- | --- | --- | --- |
| v4 | 67.3% | 11.5 points | Narrowed the customer-decision rule and added guidance for template confirmations |
| v5 | 74.4% | 16.7 points | Based Service labels on fault and set category through the task |
| v6 | 78.2% | 10.3 points | Set the order for applying category rules and added rules |
| v7 | 82.7% | 7.7 points | Clarified rules for overlapping categories and reduced the Processing gap from -5.1 to -1.3 points |

**Reading the measures:** Agreement is the share of labels that match the manual reference. Mix error tracks differences in category proportions, in percentage points. The original notes do not specify how those differences were combined into one score.

### Category gaps at v7

| Category | Difference in share vs manual labels |
| --- | --- |
| Transactional | -2.6 points |
| Processing | -1.3 points |
| None | +0.6 points |
| Growth | +2.6 points |
| Service | +0.6 points |

The original notes did not report a gap for Internal.

**What I learned:** v5 improved agreement while category mix error worsened. Checking both measures revealed a problem that agreement alone would have hidden.

### Limits

- The reference came from a single rater and contained inconsistent labels on near-identical messages. The reference labels can also be wrong.
- The reference table was deleted on October 9, 2026. These comparisons cannot be rerun, and the next prompt evaluation needs a new labelled set.
- Earlier figures combined Processing with Transactional and overstated agreement. The table above replaces those figures.

## Full backfill audit

- **Run:** October 7, 2026; v7 with ten Claude Opus subagents. Backfill means classifying the historical messages.
- **Historical processing:** 3,579 messages across 1,062 conversations; all task names were on the approved list.
- **Audit:** A separate read-only AI agent reviewed 40 randomly selected records.

### Results

| Check | Agreement |
| --- | --- |
| Category | 39 of 40 |
| Task | 38 of 40 |

### Findings and follow-up

- **Service under-labelling:** Estimated rate of 3.0–3.5%, compared with 2.6% classified.
- **Consistency across batches:** Five differences in how tasks were labelled, including incoming purchase orders.
- **Response:** Added temporary guidance to the daily prompt.

### Limits

- The sample was small and reviewed by AI. A human did not verify the accuracy figures.
- The estimated Service rate was not measured across the full dataset.
- Using an approved task name does not mean the task was correctly identified.

## How distinct are the categories?

- **Date and sample:** September 23, 2026; 420 labelled messages.
- **Method:** Category separability analysis using cosine similarity on `text-embedding-3-small` vectors. This compares numerical representations of message text.
- **Question:** Are the categories distinguishable from message text alone?

### Findings

- Growth messages were most similar to each other and most distinct from other categories.
- Transactional overlapped most with other categories and represented about half the data.

The similarity analysis pointed to a different category overlap than the actual mistakes. Reviewing those mistakes showed Service messages being labelled Processing, so I added a rule for that error.

**Lesson:** Text similarity helps reveal category overlap. It does not measure classification accuracy or replace reviewing mistakes.

## Grouping emails without preset categories

- **Date and sample:** October 2, 2026; 1,985 email embeddings after removing duplicates.
- **Method:** Unsupervised clustering in two passes. UMAP reduces the number of dimensions in the embeddings; HDBSCAN groups similar messages. No categories were supplied in advance.

### Results

| Observation | Result |
| --- | --- |
| Identified groups | 45 email types across 5 work areas |
| Messages outside a group | 5% |
| First-pass consistency across random seeds | Adjusted Rand Index (ARI) 0.89–0.96 |
| Sequence messages grouped as Outreach | 294 of 299 |

**Interpretation:** Automated sequence emails grouped together without preset labels, providing another way to check the task categories.

**Reading ARI:** Adjusted Rand Index compares how closely two groupings match. The reported range shows consistency across random seeds, not whether the groups or task labels are correct.

## Checking snapshot totals

- **Checks per refresh:** Message totals by kind, missing task labels, duplicate records, senders without a person mapping, and account matches.
- **Snapshot date:** October 16, 2026.
- **Window:** September 17–October 15, 2026.
- **Result:** All 13,117 messages were accounted for.

### Message breakdown

| Reported message grouping | Count |
| --- | --- |
| Sequence | 5,163 |
| Human sent | 4,126 |
| Incoming | 3,250 |
| Incoming automated | 552 |
| Null-minute | 24 |
| Automated | 2 |
| **Total** | **13,117** |

**Reading the breakdown:** These are the groupings reported by the snapshot. Null-minute means a duration value is missing; it is not a type of message.

**Limit:** Matching totals does not confirm correct labels, capture of all work, or accurate task times.

## Checks after changes and remaining gaps

I also reran a small, known set of cases (regression fixtures) after query changes to check for unexpected differences.

- **New reference set:** Needed for the next prompt evaluation.
- **Broader coverage:** Testing across more roles and collecting more time studies would show whether the approach works beyond the original sample.
- **Business outcomes:** Time saved and leadership decisions changed have not been recorded.
