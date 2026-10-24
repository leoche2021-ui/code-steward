# Evidence for consequential changes

## Deletion and simplification

Search the symbol, path, configuration key, and alternative spellings. Inspect callers and registration mechanisms: reflection, dependency injection, route discovery, plugin loading, code generation, serialization, environment-specific entrypoints, and package exports. Consult history when the original rationale affects the decision.

Classify references as runtime, tests, examples, generated, or unresolved dynamic use. Explain the observable capability that would disappear. Retain the candidate if evidence is insufficient, especially when consumers may exist outside the repository.

When removal is justified, update the associated implementation, exclusive tests, exports, configuration, documentation, and dependency metadata together. Preserve historical migrations and compatibility obligations. Regenerate derived files through their documented tooling; do not casually hand-edit them.

Examples of useful evidence:

| Candidate | Decisive evidence |
| --- | --- |
| Duplicate state | One authority preserves all required transitions and observers |
| Unused internal helper | No static or dynamic caller, plus affected behavior checks |
| Public export | Consumer and support-contract review, plus authorized removal |
| Defensive copy | Ownership and mutation behavior remain valid without aliasing bugs |
| Custom parser | Replacement matches accepted inputs, invalid-input behavior, and limits |
| Duplicate tests | Remaining cases protect the same invariants at the necessary boundaries |

## Lifecycle and concurrency

Identify who acquires, owns, transfers, and releases each relevant resource. Examine success, partial initialization failure, cancellation, repeated initialization, and shutdown. Include stale callbacks, double settlement, retry duplication, and cleanup after exceptions when those behaviors are reachable.

For asynchronous code, verify what happens when a newer operation supersedes an older one. Cancellation is not necessarily rollback. For retries, distinguish transient failures from permanent ones and check idempotency before replaying side effects.

Useful checks exercise disposal, interrupted work, or competing updates and assert observable state or resource release. A happy-path unit test alone cannot establish lifecycle safety.

## Trust and compatibility boundaries

Check whether a seemingly redundant guard protects untrusted input, ownership, permissions, an external consumer, or a persistent format. Internal callers may still cross a real boundary. Trace the actual guarantee rather than inferring safety from process locality.

For contract changes, identify supported consumers and migration requirements. Preserve required behavior or obtain authorization for its removal. A local test suite cannot demonstrate compatibility with unknown consumers.

## Performance claims

Investigate material repeated work: excessive I/O, N+1 access, repeated rendering, unbounded queues or caches, unnecessary allocation, or duplicate network requests. Measure when performance is the reason for changing behavior.

Compare equivalent inputs and environments; record workload, method, and relevant variability. A microbenchmark does not establish end-to-end improvement. Prefer the simpler implementation when a proposed optimization has no demonstrated benefit.

## Evidence strength

| Change | Appropriate confidence source |
| --- | --- |
| Local structural cleanup | Reference analysis and focused checks |
| Behavior fix | Reproduction and regression test |
| Resource or concurrency change | Failure-path or runtime validation |
| Public contract removal | Consumer evidence and contract checks |
| Persistent format change | Compatibility and migration verification |
| Performance improvement | Comparable measurements |

Use the row relevant to the change; this is not a demand to run every category of test.
