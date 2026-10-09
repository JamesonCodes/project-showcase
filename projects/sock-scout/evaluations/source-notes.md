# Sock Scout source notes and evidence gaps

This documentation draft was adapted on October 9, 2026 from the local portfolio repository at revision `0021813abcdf870b8e0b777f0e3b6166d38c62d7`. The inspected working tree had no tracked modifications; untracked social cover images were not used. No application source, production analytics, or evaluation dataset was inspected.

## Sources

- [Portfolio featured project at the inspected revision](https://github.com/JamesonCodes/JamesonCodes.github.io/blob/0021813abcdf870b8e0b777f0e3b6166d38c62d7/index.html): focus, stack, reported adoption, speed, and lost-asset time reduction.
- [Semantic search article at the inspected revision](https://github.com/JamesonCodes/JamesonCodes.github.io/blob/0021813abcdf870b8e0b777f0e3b6166d38c62d7/articles/semantic-search-engine.html): problem, requirements, architecture, ingestion, search, flagging, reported results, and lessons.
- [Published case study](https://jamesoncodes.github.io/articles/semantic-search-engine.html): reader-facing account; the live page may change independently of the pinned snapshot.

## Evidence classification

| Claim | Source characterization | What is missing |
| --- | --- | --- |
| 1,000+ searches/week | Reported usage | Dated analytics export, event definition, and window |
| ~10× faster | Reported comparison | Baseline, task definition, sample, and method |
| 300–600 ms latency | Reported performance | Timing boundary, distribution, load, and test window |
| ~40% less lost-asset time | Approximate portfolio claim | Confirmation of whether measured or estimated, baseline, and method |
| Positive designer feedback | Qualitative feedback in article | Context and attribution permission before reproducing the quote here |
| 100k+ assets | Reported corpus scale | Dated inventory; distinguish designs, files, and embedding units |

The architecture graphic labels 75,000+ designs and the results screenshot shows 113,125 styles. Treat them as unreconciled snapshots. The article's 253k embedding units are a different unit, not an asset count.

## Next evidence to add

{Add baseline and follow-up task measurements with dates, source links, sample sizes, units, and limitations}

{Add relevance evaluation examples, failure cases, and anonymized usage exports}

Keep raw private assets and credentials out of this folder. Link the existing application repository if shareable instead of copying its source.
