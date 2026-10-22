# Certin Education

[![License: GPL v3](https://img.shields.io/badge/License-GPLv3-blue.svg)](LICENSE)
![Content](https://img.shields.io/badge/content-open%20source%20education-brightgreen)
![Format](https://img.shields.io/badge/format-Markdown-000000?logo=markdown)
![Contributions](https://img.shields.io/badge/contributions-welcome-orange)

Open-source educational content powering **Certin**, the educational study portal at https://certin.app/.

This repository is the source of the learning content published through Certin, including collections, learning paths, topics, and their associated study material. Content is authored primarily in Markdown with front matter and lightweight learning shortcodes, then promoted through the repository's development, staging, and production workflow.

> **Study the published content:** https://certin.app/

## What you'll find here

- **Topics** — focused reference material covering technologies, products, and architectural concepts.
- **Learning paths** — ordered learning experiences that connect related material.
- **Collections** — grouped resources for broader subjects and certification tracks.
- **Google Cloud certification content** — study material for tracks including Professional Cloud Architect (PCA) and Professional Data Engineer (PDE).
- **Product baseline material** — concise references across Google Cloud services and categories.

## Repository structure

```text
.
├── development/
│   ├── collections/
│   ├── learning-paths/
│   └── topics/
├── staging/
│   ├── collections/
│   ├── learning-paths/
│   └── topics/
├── production/
│   ├── collections/
│   ├── learning-paths/
│   └── topics/
└── LICENSE
```

The repository keeps content in **development**, **staging**, and **production** trees. When contributing, make source changes in `development/` unless the project's maintainers specify a different promotion workflow.

## Content format

Most resources use YAML front matter to describe the content and Markdown for the lesson itself. For example:

```markdown
---
id: python3-first-program
type: coding-tutorial
title: "Python 3: Build a Tiny Greeting Program"
difficulty: beginner
duration: 8 min
status: published
---
```

Interactive lessons may also contain project-specific shortcodes such as `step`, `hint`, and `check`, plus fenced code blocks that identify editable files or validation criteria.

When adding or editing content, preserve the existing metadata and shortcode conventions used by neighboring files.

## Content authoring model

This repository is the source of the educational content published on **Certin**. Its primary purpose is to make learning content easy to author, organise, review, and contribute to as open source material.

Content is organised in three layers:

1. **Collections** — the top-level grouping for a Learning Path or other general learning modality.
2. **Learning Paths** — structured study journeys that associate related topics for a particular learning goal.
3. **Topics** — the individual units of learning material that make up a Learning Path.

The relationship can be thought of as:

```text
Collection
└── Learning Path
    ├── Topic
    ├── Topic
    └── Topic
```

### 1. Collections

Start with a **Collection** when defining the top-level learning experience. A collection groups content around a Learning Path or another supported general modality and provides the entry point for organising related study material.

### 2. Learning Paths

A **Learning Path** brings together the topics a learner should study for a particular subject or objective. Authors use the Learning Path to associate and order relevant topics into a coherent study journey.

When authoring a Learning Path, focus on:

- a clear learning objective;
- the topics required to achieve that objective;
- a sensible progression through those topics; and
- keeping the path focused rather than duplicating learning material.

### 3. Topics

A **Topic** contains the actual learning material. Topics should be focused, reusable units of educational content that can be associated with a Learning Path.

A topic should aim to teach one clearly defined area and contain enough context for the learner to understand the material without unnecessary duplication.

## Authoring workflow

A typical contribution follows this sequence:

```text
Define or select a Collection
        ↓
Define or select a Learning Path
        ↓
Identify the Topics required for study
        ↓
Author or improve the Topic material
        ↓
Associate Topics with the Learning Path
        ↓
Review and submit the change
```

When contributing, prefer improving or reusing an existing Topic where appropriate instead of creating duplicate material. The repository structure and metadata establish the relationships between Collections, Learning Paths, and Topics.

## Contributing

Contributions that improve accuracy, clarity, accessibility, examples, exercises, or topic coverage are welcome.

1. Fork the repository and create a branch for your change.
2. Make the change in the appropriate path under `development/`.
3. Follow the metadata and formatting conventions of nearby content.
4. Keep lessons focused, technically accurate, and useful to learners at the stated difficulty level.
5. Verify code examples and commands where practical.
6. Check internal IDs, topic references, front matter, Markdown, diagrams, and shortcodes for obvious errors.
7. Open a pull request explaining what changed, why it improves the educational material, and any sources used to verify technical claims.

For new content, prefer a clear learning objective, prerequisites where needed, concise explanations, practical examples, and checks or exercises that help learners confirm understanding.

### Contribution guidelines

Please keep contributions:

- **Educational** — explain concepts rather than simply presenting answers.
- **Accurate** — verify technical claims against authoritative, current documentation when applicable.
- **Original** — do not copy copyrighted training material, exam questions, documentation, or other protected content into the repository.
- **Accessible** — use clear language, descriptive headings, meaningful link text, and readable diagrams.
- **Focused** — keep each topic or tutorial scoped to a coherent learning goal.
- **Consistent** — follow the structure, naming, front matter, and shortcode patterns already present in the repository.

If a change affects generated or promoted copies in `staging/` or `production/`, describe that in the pull request rather than assuming those copies should be edited independently.

## Certification content notice

Certification study material in this repository is intended for education and exam preparation. It should teach concepts, reasoning, and product knowledge rather than reproduce confidential or copyrighted exam questions. Certification requirements and cloud products change over time, so learners should verify current exam objectives and product behavior against the relevant official documentation.

Google Cloud product names and certification names are trademarks of their respective owners. Neither this repository nor Certin is affiliated with or endorsed by certification vendors.

## License

This repository is licensed under the **GNU General Public License v3.0**. See [LICENSE](LICENSE) for the full license text.

By contributing, you agree that your contribution may be distributed under the repository's license.

## Community

Questions, corrections, new lesson ideas, and improvements are welcome through the repository's issue and pull-request workflow. When reporting a content problem, include the affected file and enough context for another contributor to reproduce or understand the issue.

---

**Learn openly. Improve collaboratively. Share knowledge responsibly.**
