<!--
Copy this file to `skills/<skill-name>/SKILL.md`, replace every placeholder, and delete all comments.

Create a skill only when all of these are true: maintainers repeat the task; agents have a known, recurring failure; a proven correction exists; the result is reusable across projects; and the result can be verified.

This is a concise default shape, not mandatory boilerplate. Headings are optional: retain only sections that help the workflow, and remove empty sections and placeholders.
-->
---
name: <skill-name>
description: "<Describe the capability, when to use it, and realistic trigger terms.>"
license: MIT
---

# <Capability name>

## When to use

Use this skill when <describe the repeated task and the recurring failure it prevents>.

## Instructions

1. <State the proven action or guardrail.>
2. <State the next essential action.>

## Constraints

- <State only risks or limits that apply.>
- Declare any unavoidable dependencies, environment requirements, access needs, or side effects explicitly; do not hide them as assumptions.

## Expected result

- <State the observable outcome and how to verify it.>

<!--
Keep instructions focused and capability-oriented. Do not depend on a particular model, client, programming language, framework, runtime, or operating system unless that dependency is unavoidable and declared above.

Add supporting files or directories only when they contain needed content. Any local reference must use a path relative to this skill's root.
-->
