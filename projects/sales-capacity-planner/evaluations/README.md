# Evaluations

[Back to the case study](../README.md)

I evaluated classification quality, explored the task taxonomy, and checked reporting completeness separately. The evaluations used real internal email data. The methods are summarized here without publishing customer communications or company-specific results.

| Check | What I did | What it can establish |
| --- | --- | --- |
| Prompt comparison | Compared successive prompts against one account manager's manual labels, tracking agreement and category mix error separately | Whether labels match the reference and whether the distribution of work categories is distorted |
| Backfill audit | Used a separate read-only AI agent to review a random sample of classified records, checking category and task agreement and consistency across processing partitions | A limited check on the completed run; AI reviewer agreement is not human-verified accuracy |
| Category separability | Compared email embeddings using cosine similarity to explore category boundaries | Where message text is structurally ambiguous; this does not identify the actual classification errors by itself |
| Exploratory clustering | Applied UMAP and HDBSCAN to deduplicated email embeddings without supplying categories, then checked cluster stability across random seeds | An exploratory cross-check of the taxonomy, rather than a classification accuracy test |
| Snapshot reconciliation | Checked message totals by kind, unclassified records, duplicate identifiers, unmapped senders, and account matches on each refresh | Whether inputs are accounted for and mapping gaps are visible; reconciliation does not validate estimated hours |

I also used regression fixtures to check query changes. Together, these checks distinguish classification errors, data coverage gaps, and uncertainty in the effort model.

**Evaluation limits:** The manual reference came from a single rater and contained inconsistent labels. Prompt comparisons came from direct review rather than an end-to-end pipeline run. The original reference set is no longer retained, so those comparisons cannot be reproduced; a new labelled set is needed for the next evaluation. The backfill audit covered a small sample and used an AI reviewer. These checks do not establish general accuracy across all roles or future email.

