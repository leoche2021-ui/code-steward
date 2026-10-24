---
name: code-steward
description: Perform an evidence-based hardening and simplification pass on an implementation or worktree. Use when asked to review and fix correctness, regression coverage, lifecycle failures, or unnecessary complexity after implementation. Keep changes within the requested behavior and affected surface.
metadata:
  version: "2.1.0"
---

# Code Steward

Improve the engineering quality of a bounded change through demonstrated findings, minimal fixes, and proportionate verification. The result is a justified diff and an honest account of what was verified.

## Establish scope and baseline

Read the user's request, repository instructions, working-tree status, relevant diff, callers, and tests. Determine whether the request permits fixes or asks for review only. Respect that mode. If no comparison base is supplied, inspect repository context before choosing one and state any material assumption.

Identify existing user edits without overwriting them. Distinguish generated files, vendored code, public interfaces, migrations, and persistent formats. Discover actual project validation commands from repository configuration and documentation rather than guessing them.

Run a proportionate baseline where practical. Record pre-existing failures and unavailable checks. If a failure's origin is uncertain, say so; reproduce against an isolated baseline when necessary without resetting the user's workspace.

## Follow evidence, not a cleanup quota

Prioritize correctness, trust and ownership boundaries, regression protection, simplicity, maintainability, then measured performance. Inspect the affected behavior: inputs, outputs, side effects, state transitions, error paths, resource ownership, and external contracts.

For each material candidate, establish:

- A concrete trigger or a demonstrated unnecessary maintenance burden.
- Evidence that the affected path is relevant to the requested change.
- The smallest intervention that addresses the cause.
- A check capable of distinguishing the intended result from a regression.

Implement authorized fixes, validate, then inspect their interactions with the rest of the diff. Keep a short findings record for substantial work; do not manufacture ceremony for small fixes. Defer unrelated problems rather than expanding into a repository-wide rewrite.

## Choose the relevant depth

Read [the evidence guide](references/evidence-guide.md) for deletion, lifecycle, contract, or performance changes. Focus on plausible failure modes in the affected system rather than applying every checklist item everywhere.

Reduce duplicate sources of truth when they actually create synchronization risk. A single caller, wrapper, or interface is a review signal, not proof that an abstraction is unnecessary. Keep useful domain names and ownership boundaries.

Before deleting a material path, check dynamic use and external obligations. Absence from a text search does not prove an exported API is unused. Preserve validation, accessibility, authorization, isolation, persistence compatibility, and cleanup unless their replacement or redundancy is established. A supported capability removal needs authorization for that behavior change.

Do not add dependencies, redesign architecture, remove features, alter public contracts, or change persistent data merely to make cleanup easier. Propose out-of-scope changes separately while completing in-scope work.

## Ask when the user owns the tradeoff

Use an available structured question tool at any stage when a finding exposes a meaningful choice about intended behavior, compatibility, scope, or engineering cost that existing instructions do not settle. Present two or three feasible options, recommend one with a concrete reason, and explain the practical consequence of each. Respect the host tool limits and allow a custom answer. If no suitable tool is available, ask a concise multiple-choice question in the conversation.

Investigate facts first. Continue already authorized fixes and independent checks while a question is pending; wait for a required answer before making the dependent change. Do not treat silence or a preselected option as approval, repeat settled choices, or ask the user to decide routine implementation details. Use the required approval mechanism for actions needing permission.

## Verify behavior

For a bug fix, prefer a regression check that fails for the old behavior and passes for the fix. Use the lowest testing layer that exercises the relevant contract. Extend existing coverage when suitable. Test observable outcomes, including meaningful failure paths; do not add tests solely to assert implementation text or increase coverage numbers.

When necessary, demonstrate test sensitivity in an isolated copy or with a narrowly reversible edit. Never intentionally break shared work or leave a mutation behind. Do not delete tests merely because they look similar: first identify the distinct invariant, environment, or integration boundary each protects.

Run the narrow decisive checks first, then required repository checks and broader validation justified by the affected surface. Verify combined changes. Review the final diff and run `git diff --check` when Git is available. Do not rerun expensive checks without a new change, failure, or unresolved concern.

When checks fail, determine whether the change caused the failure, fix in-scope regressions, and rerun relevant checks. Do not weaken assertions or bypass checks to obtain a green result. Report blocked validation with its practical impact.

## Stop at an evidence-based boundary

Review the final diff afresh for correctness, failure handling, resource lifetime, regression gaps, contract changes, and accidental scope expansion. Continue when this reveals a concrete material issue in scope.

Stop when known in-scope issues are addressed or explicitly blocked, relevant checks have passed or their limits are recorded, and further changes are speculative or cosmetic. This is not a claim that all possible bugs have been exhausted. Do not start goal mode, persistent monitoring, deployment, or publication solely because this skill is invoked.

## Report the result

State the meaningful changes and why they matter; list checks actually run and their outcomes. Separate fixed issues, pre-existing failures, unresolved risks, and candidates retained for lack of evidence. In review-only mode, report actionable findings with a trigger, impact, and location; do not edit files.

If no change is justified, say so. Do not claim production readiness, comprehensive security, or improved performance beyond the evidence collected.
