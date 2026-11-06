# Prompt — first audit (paste into Copilot with the custom agent selected)

Use `django-hexagonal-quality-auditor` in STRICT READ-ONLY REVIEW mode.

Review the recently refactored Redis exception handling in this Django project, including affected hexagonal architecture layers, Django/Redis/Celery integrations, public contracts, and regression risks.

Read `docs/ai-review/AUDIT_SCOPE.md` and `.github/skills/django-hexagonal-quality-audit/SKILL.md`. Discover the real architecture, impacted files, test setup and baseline; do not invent missing details.

**Never edit/create/delete files, run shell commands/tests, apply patches, format, commit, or implement fixes.** Report exclusively in chat.

I need a rigorous, balanced report with two explicit parts: (A) what is already well implemented, with evidence; (B) what is incorrect, fragile, poorly organized, insufficiently tested, or could be improved, with severity, precise locations, risks and actionable recommendations. Distinguish confirmed defects from risks and optional improvements. Review architecture, correctness, Python quality, SOLID/DRY/KISS/YAGNI, exceptions, Redis outages/cache misses/false 404, Celery, security, tests, line+branch coverage goal, formatting and lint. Mark unexecuted checks NOT RUN.

Prioritize a correction plan for a separate AI fixing agent. Stop after the report and wait for my next review request.

---

# Prompt — subsequent audit (paste after a separate agent has fixed approved issues)

Use `django-hexagonal-quality-auditor` in STRICT READ-ONLY REVIEW mode.

A separate agent has applied corrections since the previous audit. Perform a fresh independent review of the current code and affected callers. Compare against the previous audit report included in this conversation (if available); otherwise request that report and still review the current code.

For each previous finding ID, classify RESOLVED / PARTIALLY RESOLVED / STILL OPEN / REGRESSED / NOT VERIFIED / SUPERSEDED with code evidence. Look for NEW bugs, architectural violations, exception mishandling, Redis/Celery regressions, broken contracts, missing tests, and quality issues introduced by fixes.

Report again: (A) what is now well handled; (B) remaining defects and improvements; (C) previous finding status; (D) regression risks; (E) checks that are NOT RUN or UNVERIFIED; (F) prioritized next correction plan.

No file changes, commands, tests, patches, formatting or commits. Output the report in chat only.
