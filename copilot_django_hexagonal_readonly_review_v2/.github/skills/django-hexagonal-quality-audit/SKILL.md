---
name: django-hexagonal-quality-audit
description: Read-only, evidence-based Django hexagonal architecture code review with positive findings, defects, Redis/Celery failure analysis, regression assessment and iterative review rounds.
---

# Protocol — independent audit, no fixes
Read `docs/ai-review/AUDIT_SCOPE.md`. This skill is analysis-only. Do not call write/edit/execute tools, create files, or implement recommendations. Report in chat.

## Phase 1 — Scope and baseline
- Identify target feature, change boundaries, repository revision and baseline evidence. Inspect current changes and relevant call graph using available read/search capabilities; if Git commands are unavailable, inspect exposed Git metadata/diffs or request them.
- Enumerate dependencies and affected consumers, public interfaces, settings, and test coverage. Identify uncertainties without inventing paths or requirements.
- Check project-specific conventions in docs, ADRs, configuration, CI, and representative code.

## Phase 2 — Hexagonal architecture
- Map domain entities/value objects/services, use cases, inbound/outbound ports, adapters, DI/composition root, Django integration and infrastructure.
- Verify direction of dependencies, separation of domain/application/infrastructure, business exception vs technical exception, DTO mapping, validation ownership, transaction boundaries, contract fidelity and test seams.
- Prefer documented project conventions over a generic folder structure. Identify strengths as well as genuine violations. Flag speculative abstractions as optional, not mandatory.

## Phase 3 — Correctness and Python quality
- Examine success/failure paths, invariants, None/sentinel semantics, missing validation, mutable defaults, side effects, type hints, public signatures, naming, cohesion, dead code, duplication, unreachable branches, control-flow complexity and hidden coupling.
- Evaluate SOLID, DRY, KISS, YAGNI and Pythonic style pragmatically. Identify overengineering, unnecessary indirection and unjustified design patterns.
- Check exception scope and chaining, swallowed errors, wrong HTTP mappings, unexpected exceptions, logs and secrets, race conditions, timeouts and resource cleanup.
- Check Django ORM query behavior, N+1, transactions, permissions, serializer validation, authentication, CSRF where relevant, SQL safety and data integrity.

## Phase 4 — Redis and Celery reliability
- Trace cache hit, miss, Redis outage, timeout, stale/invalid payload, serialization failure, invalidation, TTL, concurrency, stampede, unexpected programming error and backend configuration including `IGNORE_EXCEPTIONS` where present.
- Distinguish cache optionality from Redis as broker/result backend/lock. Inspect exception translation, fallback, monitoring, HTTP contract and false-404 risk. Do not prescribe 503/fallback/custom exception without documented contract.
- For Celery inspect task signatures, retries/backoff/jitter, idempotency, duplicate delivery, `transaction.on_commit`, transaction timing, task result visibility, time limits, queue routing, serialization and worker failure.

## Phase 5 — Regression analysis
- Compare before/after behavior when reliable baseline evidence exists. Identify altered contracts, affected consumers and previously passing scenarios.
- Prioritize tests for: resource exists + Redis down; genuine missing resource; cache miss; Redis timeout; unexpected exception; stale cache; retry/duplicate task; concurrent requests; permissions; response compatibility.
- Distinguish code-level regression risk from experimentally confirmed regression. Do not assert absence of regression without evidence.

## Phase 6 — Test and quality gate audit
- Inspect test configuration, unit/integration/contract tests, fixtures, mocking realism, negative paths, deterministic isolation, flaky tests, assertions and missing scenarios.
- Identify configured test, lint, formatter, typing, security and coverage tools. **Never run commands yourself.**
- Recommend check-only commands for a human/isolated CI runner. Note pytest and coverage can write artifacts; production isolation is mandatory.
- Aim for measured 100% statement and branch coverage of explicitly defined critical changed scope, report actual measured numbers only from supplied evidence; global coverage separate. Coverage does not prove correctness.

## Phase 7 — Balanced report
- Include evidenced strengths with locations and rationale, not empty compliments.
- Each finding: `ID`, severity P0/P1/P2/P3, category, status, exact path/line or closest location, evidence, behavior/risk, affected contracts, recommendation (text only), verification/test, confidence, introduced/pre-existing/unknown.
- P0: critical security/data loss/production outage. P1: significant correctness/regression. P2: moderate maintainability/reliability. P3: minor style/documentation.
- Keep optional improvement separate from confirmed defect. Avoid duplicating findings. Rank by user impact and risk, not number of style warnings.
- For iterative rounds, compare previous IDs and document `RESOLVED`, `PARTIALLY RESOLVED`, `STILL OPEN`, `REGRESSED`, `NOT VERIFIED`, `SUPERSEDED`, plus NEW findings.
- End with actionable handoff to a **separate fixing agent**, no code changes.
