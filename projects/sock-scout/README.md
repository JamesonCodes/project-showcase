# Sock Scout

![Sock Scout dark logo](screenshots/logo-dark.png)

An internal semantic visual search tool that helps Sock Club’s design and sales teams find relevant work across a creative archive of 100k+ assets.

## Metadata

| Field | Value |
| --- | --- |
| Documentation status | Published |
| Project status | Deployed and used daily by the team |
| My role | Defined requirements with designers and sales; built the search system and asset flagging workflow |
| Timeline | Sales feature functionality: 2 weeks. Design feature functionality: 1 month. Both developed part-time. |
| Tools | Next.js / React, TypeScript, FastAPI, Vercel, Vertex AI, Pinecone, AWS S3, AWS Cognito, HubSpot API, PostHog |

## Problem and solution

- **Users and previous workflow:** Sock Club designers, sales teammates, and new hires browsed nested Dropbox folders, guessed filenames, or asked colleagues to locate past creative work.
- **Friction:** Designers recreated hard-to-find assets; sales interrupted designers for examples; new hires relied on tribal knowledge.
- **What changed:** Teammates search by meaning and visual similarity, rather than relying on exact filenames or tags. They can describe a concept, enter a client name, upload an image, or find designs similar to an existing result. Results include previews, original files, and related HubSpot or internal project context.
- **Human judgment:** Teammates choose suitable designs and flag issues such as outdated logos, licensing restrictions, or knittability. A similarity score alone does not establish production suitability.

## My contribution

- **Personal responsibilities:** Worked with design and sales to define requirements; built the end-to-end search system, resilient ingestion pipeline, and asset flagging workflow.
- **Collaborators:** Designers and sales informed requirements. Baylor Meche and Rachal Berry created the logo.
- **AI assistance:** Used Codex and Claude for AI-assisted development, research, learning, and understanding the technologies and implementation. Vertex AI provides the product’s runtime multimodal embeddings.

## Demo

The screenshots below walk through a search for an existing client's designs.

1. **Input:** Search for `Denver airport`.
2. **System behavior:** Return matching designs in a results grid with similarity scores and visible quality flags.
3. **Outcome:** A teammate can inspect a candidate, open its deal or portal context, download the PSD, or explore similar designs. This walkthrough illustrates the interface rather than a timed task.

![Sock Scout home screen with text and image search](screenshots/home-dark.png)

*Search entry point. Original screenshot; capture date and real-versus-synthetic provenance are undocumented.*

![Results for Denver airport with similarity scores and flagged assets](screenshots/results-dark.png)

*Search results for Denver airport. The screenshot shows 113,125 styles searched at the time of capture; it is not a current inventory.*

![Asset detail view with deal links, PSD download, and similar-design controls](screenshots/asset-details-dark.png)

*Sanitized screenshot: deal name and owner are blurred. Capture date and other sanitization details are undocumented.*

See the [screenshot index](screenshots/README.md) for the flagging view and source files.

## How it works

![Sock Scout system architecture](diagrams/architecture.png)

*Architecture diagram. Corpus counts reflect different historical snapshots; see the [diagram notes](diagrams/README.md) for context.*

- **Components:** Next.js frontend; FastAPI search backend on Vercel’s serverless Python runtime; Vertex AI embeddings; Pinecone serverless vector index; S3 asset storage; Cognito authentication.
- **Integrations:** Dropbox-to-S3 ingestion and HubSpot deal metadata.
- **Decision logic:** Text and image queries share an embedding space. The index uses cosine similarity and 1,408-dimensional vectors, with metadata filtering and hydration.
- **Ingestion:** Convert files to PNG previews, generate embeddings, and upsert vectors with metadata. Check Pinecone before embedding to avoid duplicates.
- **Error handling:** Adjustable batch concurrency, exponential backoff and retries, corrupt-file skipping, blank-PSD handling, and progress tracking support long ingestion runs.
- **Monitoring:** PostHog provides usage analytics and error tracking.

## Results and evidence

The figures below were previously published in my portfolio. Search-speed and lost-asset time improvements are approximate estimates based on team feedback about the previous and current workflows, rather than formal timing studies.

| Metric or observation | Before | After | Evidence type | Measurement period | Source |
| --- | --- | --- | --- | --- | --- |
| Search speed | Manual search through folders and filenames | Estimated ~10× faster | Team-informed estimate | Not supplied | [Article](https://jamesoncodes.github.io/articles/semantic-search-engine.html) |
| Internal search activity | Not supplied | 1,000+ searches/week | Usage figure; raw counts not included | Weekly unit; exact window not supplied | PostHog analytics |
| Search latency | Not supplied | 300–600 ms | Performance figure; timing boundary and distribution not documented | Not supplied | PostHog performance events |
| Lost-asset time | Time spent locating hard-to-find assets | Estimated ~40% reduction | Team-informed estimate | Not supplied | [Portfolio](https://jamesoncodes.github.io/#featured-project) |
| Designer experience | Redundant recreation and interruptions | Positive feedback and adoption | Qualitative feedback | Not supplied | [Article](https://jamesoncodes.github.io/articles/semantic-search-engine.html) |

## Decisions and lessons

- **Purpose-built search:** Dropbox Dash did not meet the team's requirements for conceptual visual discovery. Building a dedicated system meant taking ownership of ingestion, access, and reliability.
- **Shared text/image embeddings:** Vertex AI supports both query types in a shared space. I chose it for embedding quality, latency, and cost. The embedding model ranked #1 on MTEB at the time.
- **Serverless vector search:** Pinecone was chosen for metadata filtering, read performance, upserts, and low operational overhead.
- **Workflow integration:** Bringing discovery, downloads, CRM context, and quality flags together makes search useful within the team’s existing work.

- **Lessons:** UX drives adoption; resilient pipelines matter; useful search can reduce dependence on perfect filenames and metadata; trust in retrieval opens additional workflows.

## Supporting materials

- [Screenshots](screenshots/README.md)
- [Diagrams](diagrams/README.md)
- [Original portfolio case study](https://jamesoncodes.github.io/articles/semantic-search-engine.html)
