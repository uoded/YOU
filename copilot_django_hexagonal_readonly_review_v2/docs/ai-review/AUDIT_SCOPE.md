# Audit Scope — Django Hexagonal Architecture (review-only)

## Feature and historical incident
Audit the recently refactored Redis failure/exception handling in the existing Django application and all directly or indirectly affected code paths. Historical issue: `IGNORE_EXCEPTIONS=True` could mask Redis failures and, in some flows, lead to false business-not-found/HTTP 404 responses. Verify whether the current implementation fixes this without creating regressions.

## Scope discovery
- Identify relevant Django API/views, application use cases, domain exceptions, ports, adapters, Redis clients/cache, Celery tasks, settings, tests and affected callers from the actual repository.
- Identify modified paths and the pre-refactoring Git baseline from available evidence; if baseline is ambiguous or unavailable, mark `UNVERIFIED` and do not invent a comparison.
- Respect actual hexagonal architecture, ADRs, project conventions and public contracts. Avoid unrelated refactoring and speculative abstractions.

## Behavior and contracts
- Differentiate cache miss, Redis outage/timeout, unexpected infrastructure failure and genuine business not-found. Review custom exception classes actually present, their translation/chaining and HTTP mappings.
- Redis outage must not cause a false 404 solely due to infrastructure failure.
- Do not assume cache misses necessarily raise an exception, Redis must always fail open, or Redis failures must always produce 503: establish contracts from project evidence, otherwise mark `UNVERIFIED`.
- Inspect Redis roles (cache, broker, result backend, locks, sessions as applicable), Celery task boundaries, retries, idempotence, transaction-on-commit and duplicate execution.
- Preserve existing API responses, business behavior, schemas, key formats, Celery task signatures, security, dependencies and architecture.

## Review expectations
- Explicitly report both **correctly implemented aspects** and **defects/risks**, with evidence.
- Audit clean code, Pythonic/PEP conventions, SOLID/DRY/KISS/YAGNI, overengineering, validation, dead code, exceptions, Django ORM, performance, security, logging and observability.
- Identify missing tests and regression scenarios. Target 100% statement and branch coverage of critical changed scope as a quality goal, not an unverified claim.
- Identify project-configured tests, coverage, lint, formatting and type checks; do not run them. Request results from a human or isolated CI if needed.
- On later rounds, compare supplied prior report with current code, verify actual resolutions and search for new regressions.

## Strict safety and deliverable
- **READ-ONLY REVIEW ONLY**: no file creation/editing/deletion, no patches, no formatting, no terminal commands, no tests run, no migrations, no commits, no external writes.
- Output the entire audit in the conversation, including positive findings, prioritized defects, optional improvements, coverage/test status, unresolved assumptions and an actionable correction plan for another agent.
- If evidence is unavailable, use `UNVERIFIED` or `NOT RUN`; never infer unknown requirements.
- Do not perform or initiate any fixes. Stop after the report.
