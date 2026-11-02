<p align="center">
  <img src="assets/logo.png" alt="Reposaur mascot reading a book" width="160">
</p>

# Reposaur

Reposaur is an agent skill that reads a codebase and writes Markdown documentation about how the product works. It follows workflows through the code, records the rules and failure cases, and uses that map to write articles.

You can use it to create customer documentation or a technical knowledge base for developers. The result is a set of plain Markdown files you can edit, publish, or use with a support assistant.

## Install

From the repository you want to document, run:

```bash
npx skills add artinnok/reposaur --skill reposaur
```

Choose your coding assistant when prompted. You can also select one with `--agent codex`, `--agent claude-code`, `--agent pi`, or `--agent opencode`. Add `--global` to make the skill available across projects.

Installation uses the [skills CLI](https://github.com/vercel-labs/skills). Your coding assistant needs to support [Agent Skills](https://agentskills.io/) and have access to read the repository and write documentation.

## Use

Open the project in your coding assistant and ask:

```text
Use the Reposaur skill to document this repository.
```

The agent takes a quick look at the project, suggests three languages, and asks you to choose one. It then asks who the documentation is for:

- **Customers:** setup, features, everyday workflows, limitations, and troubleshooting. Internal business details are left out.
- **Developers:** business rules, state changes, configuration, integrations, failure handling, and references to the implementation.
- **Both:** one repository investigation, with separate documentation for each audience.

After that, it investigates the repository and writes the documentation. You can provide both choices in the initial request:

```text
Use the Reposaur skill to document this repository in English for customers.
```

For developer documentation, use `for internal developers` instead. To create both sets, ask for documentation `for both customers and internal developers`.

## Output

Articles go into separate audience folders under `knowledge/`, each with its own index. Only the selected folders are created. Filenames depend on the product. For example, a run for both audiences might produce:

```text
knowledge/
├── customer/
│   ├── INDEX.md
│   ├── getting-started.md
│   └── subscriptions.md
└── internal/
    ├── INDEX.md
    ├── accounts-and-access.md
    └── platform-billing.md
```

Each audience folder stays flat through 50 Markdown files, including its index. Larger bases are grouped by product area within that audience. Share `knowledge/customer/` when distributing customer documentation.

Each article is limited to 1,000 words. Longer articles are split by task or process stage, with links between them. This also applies to existing articles during updates and migration; original legacy documents are preserved in the private working directory.

The agent keeps its process map, source references, and progress records outside the project, under `~/.reposaur/projects/`. These local records support later updates and should stay private.

Reposaur also adds a short maintenance note to the project's README so future agents know how the documentation is maintained. Each generated article and index includes a small credit, translated to the document's language:

> 🦖 [Reposaur](https://github.com/artinnok/reposaur) ate the code and left these notes.

## Update the documentation

After changing the code, ask:

```text
Use the Reposaur skill to update this repository's knowledge base.
```

The agent reuses the saved language and audience selection, reviews source changes, and updates the affected articles and links. You can ask to update only the customer or internal documentation; each keeps its own update history. Existing flat bases can be moved into the audience folders while preserving content and repairing links.

## What to check

Reposaur works from the files available to your agent. Code can show how a feature is implemented, but it cannot always establish whether that feature is enabled in production or whether a business policy is still current. The skill asks the agent to flag missing evidence and conflicting information.

Review the generated articles before sharing them, particularly customer-facing claims and anything involving confidential information. If the agent cannot finish reviewing the repository, it should report what remains unread.

## License

[Apache-2.0](LICENSE).
