# Working in this repository

This public, solo-maintained repository collects practical utilities for repeated tasks that agents commonly handle poorly. Before changing a skill, read [the compatibility policy](docs/compatibility.md), then [the skill style guide](docs/skill-style-guide.md), then [the official template](template/SKILL.md).

## Create or change skills

Create a skill only when all of these are true:

- The maintainer repeats the task.
- Agents have a known recurring failure on it.
- A correction or guardrail has proven effective.
- The workflow is reusable across projects.
- The outcome can be verified.

Put each canonical skill at `skills/<skill-name>/SKILL.md`. Start from the official template. Use YAML frontmatter with only `name`, a one-line YAML-safe `description`, and `license: MIT`; the lowercase kebab-case name must match its directory. Do not add author, version, keywords, `allowed-tools`, changelogs, or skill-registration metadata.

Keep general workflows model-, client-, and technology-stack agnostic. Isolate and explicitly declare any unavoidable executable, network, credential, operating-system, or other environment dependency.

Keep the essential workflow in `SKILL.md`. Add `references/`, `assets/`, or `scripts/` only when they contain needed supporting material; do not create empty directories. Use paths relative to the skill root for local resources.

## Verify and finish

Perform structural and behavioral checks proportional to the change, including resolving every local link and path. Run repository validation once a real validation command is documented; do not assume or invent one.

Do not edit or commit generated local metadata in `.atl/`; respect [.gitignore](.gitignore). Keep the repository easy to maintain: avoid unnecessary contribution process, ownership files, per-skill release history, and manual skill catalogs or indexes.

When changing skills, report the changed paths, verification performed and results, unresolved risks or dependencies, and any supporting resources added. Do not manually index skills.
