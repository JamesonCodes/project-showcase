# Evaluations

[Back to the case study](../README.md)

These evaluations used **real internal email data**. Raw messages, ground-truth tables, and customer communications remain private.

## Evaluation map

| Evaluation | Scope | What it checks |
| --- | --- | --- |
| [Prompt comparisons](#classifier-prompt-comparisons) | 156 manually labelled messages | Label agreement and category mix |
| [Backfill audit](#full-backfill-audit) | 40 sampled records from 3,579 messages | AI reviewer agreement and consistency |
| [Category separability](#category-separability) | 420 labelled messages | Ambiguity in embedding space |
| [Unsupervised clustering](#unsupervised-clustering) | 1,985 deduplicated emails | Exploratory taxonomy check |
| [Snapshot reconciliation](#live-snapshot-reconciliation) | 13,117 messages | Record completeness |

These checks do not measure business impact or validate estimated hours. Sources are my internal prompt documentation, backfill audit, embedding analyses, and snapshot notes.

## Classifier prompt comparisons

- **Reference:** One account manager's hand-labelled time-study log, recategorized under the current six-category taxonomy.
- **Sample:** 156 messages carrying both a manual label and a classifier label.
- **Reviewed:** September 22–23, 2026, through direct message review rather than an end-to-end pipeline run.

### Results

| Prompt version | Agreement | Category mix error | Main change |
| --- | --- | --- | --- |
| v4 | 67.3% | 11.5 points | Narrowed the customer-decision rule and added guidance for template confirmations |
| v5 | 74.4% | 16.7 points | Made service classification depend on fault and derived category from task |
| v6 | 78.2% | 10.3 points | Introduced explicit decision-tree precedence and additional rules |
| v7 | 82.7% | 7.7 points | Refined boundary rules and reduced the Processing gap from -5.1 to -1.3 points |

**Reading the measures:** Agreement measures matching labels. Mix error tracks distortion in category distribution, in percentage points; the supplied notes do not specify its aggregation formula.

### Category gaps at v7

| Category | Share gap vs manual labels |
| --- | --- |
| Transactional | -2.6 points |
| Processing | -1.3 points |
| None | +0.6 points |
| Growth | +2.6 points |
| Service | +0.6 points |

An Internal gap was not included in the supplied notes.

**What I learned:** v5 improved agreement while category mix error worsened. Measuring both exposed a regression that agreement alone would have hidden.

### Limits

- The reference came from a single rater and contained inconsistent labels on near-identical messages. It is an imperfect reference rather than unquestioned ground truth.
- The reference table was deleted on October 9, 2026. These comparisons cannot be reproduced, and the next prompt evaluation needs a new labelled set.
- Earlier figures combined Processing with Transactional and overstated agreement. The table above replaces those figures.

## Full backfill audit

- **Run:** October 7, 2026; v7 with ten Claude Opus subagents.
- **Coverage:** 3,579 messages across 1,062 conversations; zero invalid task names.
- **Audit:** A separate read-only AI agent reviewed 40 randomly selected records.

### Results

| Check | Agreement |
| --- | --- |
| Category | 39 of 40 |
| Task | 38 of 40 |

### Findings and follow-up

- **Service under-labelling:** Estimated rate of 3.0–3.5%, compared with 2.6% classified.
- **Partition consistency:** Five inconsistencies, including different treatment of incoming purchase orders.
- **Response:** Added interim conventions to the daily prompt.

### Limits

- The sample was small and AI-reviewed; agreement is not human-verified accuracy.
- The Service rate is an audit estimate, not a measured population rate.
- Valid task names establish inventory compliance, not correct classification.

## Category separability

- **Date and sample:** September 23, 2026; 420 labelled messages.
- **Method:** Cosine similarity on `text-embedding-3-small` vectors.
- **Question:** Are the categories distinguishable from message text alone?

### Findings

- Growth was the most cohesive category and had the clearest boundaries.
- Transactional was the least distinct category and represented about half the data.

The separability ranking pointed toward a different boundary than the actual errors. Reviewing misclassifications showed Service messages being labelled Processing, which led to a targeted prompt rule.

**Lesson:** Embedding separability can reveal structural ambiguity, but it does not replace inspecting classifier mistakes or measure classification accuracy.

## Unsupervised clustering

- **Date and sample:** October 2, 2026; 1,985 deduplicated email embeddings.
- **Method:** Two-pass UMAP and HDBSCAN, with no categories supplied in advance.

### Results

| Observation | Result |
| --- | --- |
| Identified groups | 45 email types across 5 work areas |
| Messages outside a group | 5% |
| First-pass stability across random seeds | Adjusted Rand Index (ARI) 0.89–0.96 |
| Sequence messages grouped as Outreach | 294 of 299 |

**Interpretation:** Sequence grouping provided an independent exploratory check on the taxonomy.

**Limit:** Stability across seeds measures consistency, not group correctness or classifier accuracy.

## Live snapshot reconciliation

- **Checks per refresh:** Message totals by kind, unclassified rows, duplicate identifiers, unmapped senders, and account matches.
- **Snapshot date:** October 16, 2026.
- **Window:** September 17–October 15, 2026.
- **Result:** All 13,117 messages reconciled.

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

**Reading the breakdown:** These are the snapshot's reported groupings. Null-minute is a duration-data condition rather than a communication type.

**Limit:** Reconciliation confirms that records are accounted for. It does not establish correct labels, complete capture of all work, or accurate durations.

## Regression checks and remaining gaps

I also used regression fixtures to check query changes.

- **New reference set:** Needed for the next prompt evaluation.
- **Broader coverage:** More roles and time studies are needed to assess generalization.
- **Business outcomes:** Time saved and leadership decisions changed have not been recorded.
