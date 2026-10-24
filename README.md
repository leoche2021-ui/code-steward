# Code Steward

**Harden and simplify a change with evidence you can inspect.**

Code Steward is an agent skill for the engineering work between “the feature works” and “this change is ready for an informed review.” It finds concrete weaknesses in the affected code, applies proportionate fixes when authorized, and reports the verification behind the result.

Use it after implementing a feature, fixing a bug, or completing a refactor. It is especially useful when error paths, asynchronous cleanup, duplicate state, or abandoned implementation attempts deserve a focused second look.

## What it improves

| Area | Focus |
| --- | --- |
| Correctness | Reproducible failures and violated invariants |
| Regression protection | Tests that detect meaningful behavior changes |
| Resource lifetime | Cleanup, cancellation, partial failure, and stale work |
| Simplicity | Unnecessary state, indirection, or duplication with demonstrated cost |
| Safe removal | Dynamic consumers, public obligations, and end-to-end consistency |
| Performance | Material waste supported by comparable measurements |

The skill protects the user's existing work and keeps the pass within the requested behavior. It supports both review-only requests and authorized review-and-fix work.

## Example prompts

```text
Use $code-steward to harden my current uncommitted changes. Fix demonstrated
issues, preserve unrelated edits, and run the relevant project checks.
```

```text
Use $code-steward in review-only mode on this branch against main.
Focus on cancellation and resource cleanup. Do not edit files.
```

```text
Use $code-steward to investigate whether the old cache adapter can be
removed. Check dynamic consumers and compatibility obligations before
making any deletion.
```

## How the pass works

The agent establishes scope and a validation baseline, traces the affected behavior, and selects the highest-value finding supported by evidence. It makes the smallest sufficient fix, checks the behavior, and reviews the combined diff. It stops when remaining ideas are speculative, cosmetic, outside scope, or blocked by missing evidence.

A representative finding might be a stale asynchronous response overwriting a newer result. A useful fix would enforce the intended ownership of the result and add a test that reproduces competing responses. Simply renaming variables or adding a test that checks source text would not address that failure.

## Choices during the pass

When a finding requires your decision about behavior, compatibility, scope, or cost, the agent uses the available question tool with two or three options, a recommendation, and concrete tradeoffs. It can ask throughout the pass while continuing independent checks. Your answer guides the dependent change; routine authorized fixes proceed directly.

## Expected report

The final report distinguishes:

- Meaningful fixes and simplifications, with their engineering reasons.
- Checks actually run and their outcomes.
- Pre-existing failures and unavailable verification.
- Unresolved risks and deletion candidates retained because evidence was insufficient.

“No justified change found” is a valid result. A passing local test suite is not presented as proof of comprehensive security or production readiness.

## Installation

Copy this repository's contents into a skill directory named `code-steward` in your agent's configured skill location. Keep `SKILL.md`, `references/`, and `agents/` together. Invoke it by name in a host that supports named skills. Discovery and invocation syntax depend on the host.

The core workflow is in [SKILL.md](SKILL.md); consequential changes use the [evidence guide](references/evidence-guide.md). `agents/openai.yaml` supplies optional UI metadata that other hosts may ignore. This package uses portable skill frontmatter; it is not a WorkBuddy marketplace upload bundle.

## What changed from harden

This English revision condenses the original long checklist into a scoped workflow with an on-demand evidence guide. It removes automatic goal-mode activation and unbounded “exhaust every improvement” language. It adds explicit review-only handling, baseline uncertainty, combined-diff verification, and a stopping rule based on concrete findings.

Deletion guidance now treats public exports and unknown external consumers conservatively. Testing guidance emphasizes regression sensitivity and distinct behavioral coverage without demanding tests for every cosmetic change. Performance claims require measurements appropriate to the claim.

## Limits

Code Steward is not a deployment tool, formal verification system, or comprehensive security audit. It depends on available source, repository instructions, runnable checks, and known contracts. Missing integration environments or external consumers can limit the confidence of a conclusion; those limits belong in the report.

## Provenance

Adapted from the user-supplied `harden` skill and substantially revised as Code Steward. The supplied materials did not identify an upstream author or license. No new redistribution license is asserted here; upstream attribution and licensing remain unverified.
