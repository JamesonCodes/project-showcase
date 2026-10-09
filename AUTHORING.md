# Authoring case studies

Use the [project README template](templates/project-readme.md) for every case study. This library is for documentation, demos, diagrams, and evidence; link existing source repositories instead of copying their code into it.

## Replace placeholders

Replace each `{{...}}` placeholder with verified information. Keep placeholders visible while drafting; when information is unavailable, say so rather than inventing details, dates, achievements, or metrics. Explicitly mark sections that do not apply and briefly explain why.

Keep all 13 parts of the outline, from the project title and one-sentence description through supporting-material links. Describe personal contributions separately from collaborators and AI assistance, and explain what you personally validated.

Use **Documentation draft**, **In review**, or **Published** for documentation status. Record the actual project's development status independently, using an accurate description such as prototype, active development, maintained, or archived only when supported. A completed write-up does not imply a completed project.

## Add a project

1. Create a lowercase, hyphenated directory under `projects/`.
2. Copy `templates/project-readme.md` into it as `README.md` and replace the project name and description.
3. Create `screenshots/`, `diagrams/`, `evaluations/`, and `videos/`. Give each folder a short README explaining its intended contents, following the starters.
4. Replace `{{screenshots-path}}`, `{{diagrams-path}}`, `{{evaluations-path}}`, and `{{videos-path}}` in the copied template with `screenshots/README.md`, `diagrams/README.md`, `evaluations/README.md`, and `videos/README.md` respectively.
5. Fill in the case study as evidence becomes available, retaining clear draft status until reviewed.
6. Add the project's name, verified focus, documentation status, and relative README link to the [root directory](README.md).

The reusable template intentionally contains placeholder link targets. Resolve them in each project before publishing.

## Images, diagrams, and demos

Paths are relative to the Markdown file that contains the link. From a project README, embed an image like this after adding the file:

```markdown
![Workflow results with identifying information removed](screenshots/workflow-results.png)

*Sanitized example: identifying information has been removed.*
```

Link a supporting file with `[Evaluation notes](evaluations/baseline-comparison.md)`. From a supporting-folder README, `../README.md` links back to the case study. Use descriptive filenames and captions that explain what the reader should notice. Store diagram exports and their editable sources in `diagrams/`.

Prefer hosted demo links in `videos/README.md` over large committed recordings. Describe each demo's input, system behavior, and outcome. Check viewing permissions and provide screenshots when useful.

## Document evidence

For each result, record the before and after values or explicitly mark unavailable values, evidence type, measurement period, and source. Link to the relevant material in `evaluations/` or a stable accessible external source. Document methodology, sample size, baseline definition, units, and limitations so readers can understand the comparison.

- **Measured results:** Report observed values with their measurement method and source.
- **Estimates:** Label them as estimates and explain assumptions and calculations.
- **Qualitative feedback:** Label it as feedback and give context; use attributed quotes only with permission.

Do not treat a synthetic demo or an estimate as evidence of real-world performance. Describe missing evidence and unvalidated claims directly. Keep planned outcomes separate from achieved outcomes.

## Label examples and protect private information

Label examples next to the demo, screenshot, dataset, or evidence entry:

- **Real:** An actual example that is appropriate to share.
- **Sanitized:** A real example with identifying or confidential information removed or changed; explain the changes and their effect on interpretation.
- **Synthetic:** Invented inputs or data used to demonstrate behavior; do not present them as actual user activity or measured production outcomes.

Review text and assets for credentials, personal information, and confidential details before committing. The `.gitignore` covers common local secret files, but it does not inspect file contents.

## Keep the library organized

Keep one case study per project and place supporting assets in its four designated folders. Maintain each folder's README as an index when material is added. Link source repositories and hosted demos; avoid duplicate source code and large recordings.

Update the root project directory when adding, renaming, or changing documentation status. Keep filenames stable where possible; update inbound links when moving material. Before publishing, review remaining `{{...}}` placeholders, confirm evidence labels, check image rendering, and verify relative links resolve from their containing files. Template placeholders may remain in the reusable template.
