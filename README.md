# Project Showcase

This library holds deeper case studies, demos, diagrams, and evidence from my GTM engineering and applied AI projects, for prospective employers and teams looking to hire me to build a specific project. My [portfolio](https://jamesoncodes.github.io/) provides the highlights; this repository documents the work behind them.

## Project directory

The case studies below are documentation drafts. Documentation status describes the write-up; each project's actual development status is recorded separately in its metadata. Sock Scout and the email-system drafts include material adapted from the portfolio, with source notes and evidence gaps. Sample Hub and Portal+ Assist are awaiting author input.

| Project | Focus | Documentation status | Case study |
| --- | --- | --- | --- |
| Sock Scout | Semantic visual search for creative assets | Documentation draft | [README](projects/sock-scout/README.md) |
| AI Native Email System | Job-based inbox workflows, human review, and earned autonomy | Documentation draft | [README](projects/ai-native-email-system/README.md) |
| Portal+ Assist | {{Describe Portal+ Assist's focus}} | Documentation draft | [README](projects/portal-plus-assist/README.md) |
| Sample Hub | {{Describe Sample Hub's focus}} | Documentation draft | [README](projects/sample-hub/README.md) |

## Add a project

1. Create `projects/<project-slug>/` using a lowercase, hyphenated name.
2. Copy the [project README template](templates/project-readme.md) into that folder as `README.md`.
3. Add `screenshots/`, `diagrams/`, `evaluations/`, and `videos/`, each with a short README explaining its contents. The starter projects provide examples.
4. Replace placeholders with verified information and set the template's supporting-material paths to the local folder READMEs. Keep documentation status separate from project development status.
5. Add a row to the project directory above and verify all relative links.

See [AUTHORING.md](AUTHORING.md) for writing, evidence, and organization conventions.

## Repository structure

```text
project-showcase/
├── README.md
├── AUTHORING.md
├── .gitignore
├── templates/
│   └── project-readme.md
└── projects/
    ├── sock-scout/
    ├── ai-native-email-system/
    ├── portal-plus-assist/
    └── sample-hub/
```

The template provides this starting structure. Supporting folders can be omitted when they do not apply, as in Sock Scout:

```text
<project-slug>/
├── README.md
├── screenshots/
│   └── README.md
├── diagrams/
│   └── README.md
├── evaluations/
│   └── README.md
└── videos/
    └── README.md
```

The library uses plain Markdown and supporting assets. Existing source repositories are linked from the case studies rather than duplicated here.
