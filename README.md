# Reposaur <img src="assets/logo.png" alt="Reposaur mascot reading a book" width="96" align="right">

An [Agent Skill](https://agentskills.io/) that reads your codebase and writes Markdown documentation for customers, developers, or both.

## Install

```bash
npx skills add artinnok/reposaur
```

Choose your coding assistant when prompted. [More install options](https://github.com/vercel-labs/skills).

## Use

Open your project and ask:

```text
Use Reposaur to document this repo.
```

The agent suggests three languages, asks who the docs are for, then maps business processes and writes the articles.

After code changes, ask Reposaur to update the existing knowledge base.

## Output

| Audience | Knowledge base |
| --- | --- |
| Customers | `knowledge/customer/`: setup, usage and troubleshooting. |
| Developers | `knowledge/internal/`: business rules and implementation references. |

Choose either audience or both. Each folder has an `INDEX.md`.

Review generated docs before sharing. Repository code alone does not confirm what's running in production.

<details>
<summary>Files and maintenance</summary>

- Articles contain at most **1,000 words**; longer topics are split.
- Each audience folder stays flat through **50 Markdown files**, including its index.
- Working records stay outside your project in `~/.reposaur/projects/`.
- Updates preserve useful manual edits.

[Skill instructions](skills/reposaur/SKILL.md) · [Audience rules](skills/reposaur/references/audience-rules.md) · [Output format](skills/reposaur/references/knowledge-format.md)

</details>

[Apache-2.0](LICENSE)
