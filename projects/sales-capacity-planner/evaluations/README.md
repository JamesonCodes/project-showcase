# Evaluations

[Back to the case study](../README.md)

These evaluations ran on real internal email data. The figures report classification checks, exploratory analysis, and snapshot completeness. They do not measure business impact or validate estimated hours. Raw messages, ground-truth tables, and customer communications are not published.

Sources are my internal classifier prompt documentation, backfill audit, embedding analyses, and live snapshot notes. The results are summarized here; underlying records remain private.

## Classifier prompt comparisons

I compared successive prompts against one account manager's hand-labelled time-study log. The reference labels were recategorized under the current six-category taxonomy. The comparison covered 156 messages with both a manual label and a classifier label, reviewed September 22–23, 2026.

Agreement measures matching labels. Category mix error tracks distortion in the category distribution and is reported in percentage points. The supplied notes do not specify its aggregation formula.

| Prompt version | Agreement | Category mix error | Main change |
| --- | --- | --- | --- |
| v4 | 67.3% | 11.5 points | Narrowed the customer-decision rule and added guidance for template confirmations |
| v5 | 74.4% | 16.7 points | Made service classification depend on fault and derived category from task |
| v6 | 78.2% | 10.3 points | Introduced explicit decision-tree precedence and additional rules |
| v7 | 82.7% | 7.7 points | Refined boundary rules and reduced the Processing gap from -5.1 to -1.3 points |

Reported v7 category-share gaps relative to manual labels were Transactional -2.6, Processing -1.3, None +0.6, Growth +2.6, and Service +0.6 percentage points. An Internal gap was not included in the supplied notes.

**What I learned:** v5 improved agreement while category mix error worsened. Measuring both exposed a regression that agreement alone would have hidden.

**Limitations:**

- The reference came from a single rater and contained inconsistent labels on near-identical messages. It is an imperfect reference rather than unquestioned ground truth.
- These comparisons came from direct message review, not an end-to-end pipeline run.
- The reference table was deleted on October 9, 2026. These comparisons cannot be reproduced, and the next prompt evaluation needs a new labelled set.
- Earlier figures combined Processing with Transactional and overstated agreement. The table above replaces those figures.

## Full backfill audit

On October 7, 2026, ten Claude Opus subagents classified 3,579 messages across 1,062 conversations using v7. The run produced zero invalid task names.

A separate read-only AI agent reviewed 40 randomly selected records:

| Check | Agreement |
| --- | --- |
| Category | 39 of 40 |
| Task | 38 of 40 |

The audit suggested Service was under-labelled: the estimated rate was 3.0–3.5%, compared with 2.6% classified. It also identified five inconsistencies across processing partitions, including different treatment of incoming purchase orders. Interim conventions were added to the daily prompt to resolve them.

**Limitations:** This was a small sample reviewed by an AI agent. Agreement with that reviewer is not human-verified accuracy. The estimated Service rate is an audit estimate, not a measured population rate. Valid task names establish inventory compliance, not correct classification.

## Category separability

On September 23, 2026, I compared cosine similarity on `text-embedding-3-small` vectors for 420 labelled messages to explore whether categories were distinguishable from message text alone.

- Growth was the most cohesive category and had the clearest boundaries.
- Transactional was the least distinct category and represented about half the data.

The separability ranking pointed toward a different boundary than the actual errors. Reviewing misclassifications showed Service messages being labelled Processing, which led to a targeted prompt rule.

**Lesson:** Embedding separability can reveal structural ambiguity, but it does not replace inspecting classifier mistakes or measure classification accuracy.

## Unsupervised clustering

On October 2, 2026, I ran a two-pass UMAP and HDBSCAN analysis over 1,985 deduplicated email embeddings, without supplying categories in advance.

| Observation | Result |
| --- | --- |
| Identified groups | 45 email types across 5 work areas |
| Messages outside a group | 5% |
| First-pass stability across random seeds | Adjusted Rand Index (ARI) 0.89–0.96 |
| Sequence messages grouped as Outreach | 294 of 299 |

The sequence grouping provided an independent exploratory check on the taxonomy. Stability across seeds describes consistency of the clustering; it does not establish that the groups are correct or validate the classifier.

## Live snapshot reconciliation

Each refresh checks message totals by kind, unclassified rows, duplicate identifiers, unmapped senders, and account matches.

The October 16, 2026 snapshot covered September 17–October 15, 2026. All 13,117 messages reconciled to the following breakdown:

| Reported message grouping | Count |
| --- | --- |
| Sequence | 5,163 |
| Human sent | 4,126 |
| Incoming | 3,250 |
| Incoming automated | 552 |
| Null-minute | 24 |
| Automated | 2 |
| **Total** | **13,117** |

These are the snapshot's reported groupings; null-minute is a duration-data condition rather than a communication type. Reconciliation confirms that records are accounted for. It does not establish correct task labels, complete capture of all work, or accurate duration estimates.

## Regression checks and remaining gaps

I also used regression fixtures to check query changes. Classification, data completeness, and estimated effort require separate checks: success in one does not validate the others.

The next evaluation needs a new manually labelled reference set. Broader role coverage and time studies remain necessary to assess how well classification and duration benchmarks generalize. Time saved and leadership decisions changed have not been recorded.
