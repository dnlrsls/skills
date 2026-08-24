# Skill Style Guide

This repository uses the [Agent Skills specification](https://agentskills.io/specification) as its base format. This guide is the normative source for authoring and reviewing its canonical skills, optimized for portable reuse and low maintenance.

Read the [Compatibility Policy](compatibility.md) with this guide. If they differ, the compatibility policy governs portability and compatibility claims.

## Creation gate

Create a skill only for a reusable workflow, decision pattern, or project convention that benefits from agent guidance. Do not create one for a trivial, one-off task or material better served by ordinary documentation.

## Canonical layout

Each canonical skill **MUST** live at `skills/<skill-name>/SKILL.md`:

```text
skills/<skill-name>/
├── SKILL.md
├── references/  # optional
├── assets/      # optional
└── scripts/     # optional
```

`SKILL.md` **MUST** begin with YAML frontmatter followed by Markdown instructions. Its only required frontmatter is:

```yaml
---
name: example-skill
description: "Create focused release notes. Use when asked for release notes, changelogs, or version summaries."
license: MIT
---
```

Do not require an author, per-skill version, changelog, `CODEOWNERS`, Changesets, integration adapter, or contributor process. Repository history and releases provide version history.

## Names and descriptions

- `name` **MUST** use lowercase kebab-case and exactly match its parent directory.
- `description` **MUST** be one physical, YAML-safe line that clearly says what the skill does and when to use it.
- Descriptions **SHOULD** include realistic trigger terms a user or agent may say. Do not add a separate `Keywords` field.
- The portable core **MUST NOT** use experimental `allowed-tools`.

## Skill instructions

The body **MUST** communicate four concepts: when to use the skill, what to do, applicable constraints or risks, and an expected result that can be verified. Authors may choose headings and structure that suit the workflow; do not add empty boilerplate merely to satisfy these concepts.

Use direct capability language rather than client, model, or OS-specific commands. Use local paths relative to the skill root. Keep the main instructions focused; `SKILL.md` **SHOULD** remain under 500 lines, following the Agent Skills recommendation rather than a stricter hard limit.

## Resources and dependencies

Apply progressive disclosure:

- Put the essential workflow in `SKILL.md`.
- Put optional explanation, background, and edge cases in `references/`.
- Put reusable static templates, schemas, and fixtures in `assets/`.
- Put deterministic helpers in `scripts/`.

Declare dependencies and environment requirements, including executables, network access, credentials, or OS assumptions. Safety instructions **MUST** be proportional: explicitly call out destructive actions, credentials, network access, and meaningful side effects when they apply, but do not add generic warnings to low-risk skills.

## Results and verification

State an observable result and a verification method proportional to the work. Do not invent heavyweight ceremony. Canonical skills are expected to pass `skills-ref` validation when automated validation is introduced; this guide does not implement that tooling.

## Author review checklist

- [ ] The workflow is reusable and belongs in a skill.
- [ ] The directory, name, and minimal frontmatter are correct.
- [ ] The one-line description explains the action, use case, and realistic triggers.
- [ ] The body covers use, action, relevant risks, and a verifiable result.
- [ ] Instructions are portable, dependencies are declared, and resources are placed appropriately.
- [ ] Local references resolve, and the skill has no unnecessary maintenance metadata or process.
