---
name: skill-creator
description: "Create focused reusable Agent Skills. Use when creating or documenting a new Agent Skill."
license: MIT
---

# Create a focused Agent Skill

## When to use

Use this skill when a repeated task needs a small, reusable guardrail against a known agent failure.

## Workflow

1. First identify the target repository and read its local authoring instructions, compatibility policy, templates, licensing, and existing skills. Local policy overrides this workflow.
2. Confirm all of the following before creating a skill:
   - Maintainers repeat the task.
   - Agents have a known recurring failure.
   - A correction or guardrail has proven effective.
   - The workflow is reusable across projects.
   - The result can be verified.
   If any condition fails, recommend ordinary documentation or repository instructions instead; do not create a skill.
3. Inspect comparable existing skills. Extend one when it already covers the failure; do not create a duplicate.
4. Use the local layout, template, and metadata rules when available. Otherwise, create the minimum open Agent Skills form: a named `SKILL.md` directory entry with `name`, `description`, and a Markdown body. Discover the applicable license or ask for it; never invent one.
5. Write only the essential workflow. State the trigger, the corrective actions, applicable limits, and a verifiable result. Use capability-oriented language, progressive disclosure, and relative paths for any local resources.

## Constraints

- Keep metadata minimal and instructions portable across models, clients, and technology stacks.
- Do not name a client or tool unless it is inherently required; declare that dependency and its environment needs explicitly.
- Add references, assets, or scripts only when they contain needed material. Do not create empty resource directories or hide dependencies.

## Verify and report

Read the finished files. Confirm the directory and name match, frontmatter satisfies the applicable policy, local links and resources resolve, and no unnecessary dependencies or duplicate skill remain. Run a repository-documented validator only when one exists; do not invent a command.

Report the changed files, policy or template used, checks and results, unresolved risks or dependencies, and supporting resources added.
