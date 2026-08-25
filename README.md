# Practical Skills for AI Agents

![Software Engineering Skills banner](skillsbanner.png)

This repository contains reusable skills for tasks that AI agents can usually complete, but often handle slowly, inconsistently, or less effectively than they should. Each skill packages a proven workflow or guardrail so agents spend less time rediscovering the right approach and produce a better result sooner.

## Purpose

- Reduce the time agents lose on common, straightforward tasks.
- Correct recurring failure modes with proven workflows and guardrails.
- Reuse effective approaches across projects instead of solving the same problem again.
- Improve results without tying the workflow to one model, client, or technology stack.

## First practical skill

[`local-dev-runner`](skills/local-dev-runner/SKILL.md) is the first practical reusable skill in this repository. It helps agents start local development environments with minimal, repository-focused discovery: it uses documented commands and matching documented platform or runtime variants, manages aggregate and service processes with ownership-safe cleanup, and keeps persistent launches out of the agent foreground channel.

When a visible terminal is needed, it supports one framed printable-ASCII status dashboard inspired by the repository banner. It reports `STARTING` before readiness, then evidence-based `READY` or `FAILED` status with actual endpoints, and does not repeat unchanged commands after deterministic failures.

[`skill-creator`](skills/skill-creator/SKILL.md) remains the guide for creating focused Agent Skills only from proven, reusable corrections rather than speculative ideas.

## Documentation

- [Compatibility policy](docs/compatibility.md) — the portable canonical skill format and compatibility-claim policy.
- [Skill style guide](docs/skill-style-guide.md) — the normative guide for authoring and reviewing canonical skills.
