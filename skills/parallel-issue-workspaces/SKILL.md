---
name: parallel-issue-workspaces
description: "Launch approved, grouped Orca issue workspaces from a visible triage report. Use when prioritizing parallel issue investigation or bounded fixes."
license: MIT
---

# Parallel issue workspaces

## Use and boundaries

Use after the latest visible triage report for the repository identifies priority, open actionable issues, and root-cause or dependency groups. Consume that report only: do not query GitHub, re-triage, reinterpret groups, or search issues or pull requests.

- Select the highest priority tier containing open actionable issues. Preserve every visible root-cause or dependency group in that tier and assign one workspace per group.
- Exclude resolved, closed, duplicate, rejected, noise, non-actionable, and terminally blocked issues. Show each exclusion with its visible triage reason.
- Pull requests and native Git worktrees are context, never blockers or exclusions. Orca 1.4.188 cannot adopt an existing native worktree.
- This workflow requires read-only access to the visible triage report, a compact inventory of native Git worktrees and Orca-managed workspaces and terminals, and the Orca CLI. It creates Orca workspaces only after explicit approval.
- Do not mutate GitHub, pull requests, or existing Git or Orca resources. Do not create a workspace, open a terminal, or contact an agent before approval.

## Preview and approval

1. Select exactly one mode before the preview. If fixes were not explicitly requested, select `investigate-only`. Select `investigate-and-fix` only when fixes were explicitly requested.
2. Take one bounded, read-only inventory to match each selected group to a native Git worktree, a managed Orca workspace, and a live terminal. Match reuse by the intended group, managed workspace, and terminal binding.
3. Classify each group:

   | Condition | Action | Reason |
   | --- | --- | --- |
   | Matching managed Orca workspace with a verified live bound terminal | `reuse` | Terminal is ready for the intended group. |
   | No matching managed Orca workspace | `create-isolated` | No managed Orca workspace exists for the group. |
   | Native worktree present and no matching managed Orca workspace exists | `create-isolated` | Orca cannot adopt the existing worktree. |
   | Matching managed Orca workspace without a verified live terminal, or unverifiable/conflicting identity or binding | `blocked` | Do not treat it as active or create a duplicate. |

4. Show one compact preview. Each row must contain group issues, pull-request context, native-worktree presence, managed Orca workspace and terminal, action and reason, and the selected mode. Include totals for `reuse`, `create-isolated`, `blocked`, and exclusions.
5. Obtain one explicit approval of the shown mode. Generic approval, continuation, or workspace approval does not authorize implementation. For example, accept `Approve investigate-only` only for investigation, or `Approve investigate-and-fix` only when that exact shown mode was selected.

## Approved execution

1. After mode-specific approval, verify the approved Orca repository ID and physical-main parent-worktree ID. Do not infer either identifier.
2. For each `create-isolated` group, run sequentially exactly:
   `orca worktree create --repo <repo-id> --name <group-name> --parent-worktree <parent-id> --agent opencode --prompt <prompt> --setup skip --json`
3. Do not append `--activate`. Verify exactly `agentTerminalHandle` in that command's JSON result. If it is absent, mark only that group failed; do not accept an equivalent field, guess a handle, retry blindly, or start diagnostics.
4. For each `reuse` group, record the previously verified binding. After a successful handle verification or a recorded reuse, immediately continue to the next approved group without waiting for investigation.
5. Isolate failures. Continue the remaining approved groups without another preview or approval, and never use a live session for automatic diagnostics.

## Bounded group prompt

Write the prompt sent to the visible OpenCode agent in professional Spanish, unless the user explicitly overrides the language for that specific launch. Its group-specific context may contain only issue numbers and titles, pull-request IDs, one triage reason, and at most three evidence references. Add the selected mode boundary and these shared prohibitions: never mutate GitHub, push, merge, or create a pull request automatically.

| Selected mode | Required boundary |
| --- | --- |
| `investigate-only` | Investigate, reproduce, and prove the root cause. Report blockers or decisions. Never edit or implement. |
| `investigate-and-fix` | Investigate, reproduce, and prove the root cause. Only when the root is proven and no product or design decision remains, implement the smallest coherent fix and run relevant tests; otherwise report the blocker or decision and stop. |

## Result

Report the selected mode; the exclusions and visible reasons; failures; and totals. Include a lightweight issue → workspace → terminal matrix with group, issues, pull-request context, native-worktree presence, managed Orca workspace, `agentTerminalHandle`, and action or status. Verify the preview selection, exact creation command, and exact handle requirement against [static scenarios](references/coverage-contract-scenarios.md).
