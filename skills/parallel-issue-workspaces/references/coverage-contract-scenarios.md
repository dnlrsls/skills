# Lightweight launcher scenarios

Use these static scenarios to review preview, approval, execution, and result semantics. They do not authorize Orca operations.

| Scenario | Required result |
| --- | --- |
| Higher tier has no open actionable issue | Skip it and select the next highest tier that does. |
| Resolved, closed, duplicate, rejected, noise, non-actionable, or terminally blocked issue | Exclude it and report its visible triage reason. |
| Several issues share a visible root-cause or dependency group | Show and use one workspace for that group. |
| Native worktree present; no matching managed Orca workspace exists | Show native-worktree presence, action `create-isolated`, and reason: Orca cannot adopt the existing worktree. |
| Pull request present | Include its ID as context; it is not a blocker or exclusion. |
| Matching managed Orca workspace with a verified live terminal | Use action `reuse` only after verifying its group, workspace, and terminal binding. |
| Matching managed Orca workspace without a verified live terminal | Use action `blocked`; do not treat it as active or create a duplicate. |
| Unverifiable or conflicting managed-workspace or terminal identity | Use action `blocked`; do not guess a binding or create a duplicate. |
| No matching managed Orca workspace | After approval, use action `create-isolated`. |
| Creation result lacks `agentTerminalHandle` | Mark that group failed; do not accept a substitute field, retry, or run diagnostics. |
| One group fails | Report the failure and continue sequentially with other approved groups without another preview or approval. |
| Generic approval | It cannot authorize implementation. Require explicit approval of the preview's selected mode. |
| `investigate-only` prompt | Write the runtime prompt for the visible OpenCode agent in professional Spanish unless the user explicitly overrides the language for that specific launch; limit group-specific context to issue numbers/titles, pull-request IDs, one triage reason, and at most three evidence references; permit investigation, reproduction, and root-cause proof only, never edits or implementation. |
| `investigate-and-fix` prompt | Write the runtime prompt for the visible OpenCode agent in professional Spanish unless the user explicitly overrides the language for that specific launch; use the same context limit; permit the smallest coherent fix and relevant tests only after root-cause proof and when no product or design decision remains. |
| Either prompt | Forbid GitHub mutation, push, merge, and automatic pull-request creation. |
| Lightweight result matrix | Represent issue → workspace → terminal with group, issues, pull-request context, native-worktree presence, managed Orca workspace, `agentTerminalHandle`, and action or status. |
