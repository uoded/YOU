# Django Hexagonal Quality Auditor — strictly read-only

## Purpose
An independent Copilot custom agent that **reviews, never fixes**. It provides evidence-backed positive observations, defects, optional improvements and regression risk analysis. Use another agent to apply approved fixes, then re-run this auditor until quality goals are met.

## Installation
Copy the `.github/` and `docs/` directories from this archive into the repository root. Do **not** overwrite unrelated existing project instructions; this archive deliberately contains no global `copilot-instructions.md` or generic Python instructions. Open Copilot Chat and select the `django-hexagonal-quality-auditor` custom agent. Paste the appropriate prompt from `PROMPT_COPILOT.md`.

## Included files
- `.github/agents/django-hexagonal-quality-auditor.agent.md`: agent role, read-only restrictions, required report.
- `.github/skills/django-hexagonal-quality-audit/SKILL.md`: detailed audit protocol.
- `docs/ai-review/AUDIT_SCOPE.md`: ready-to-use project-specific audit scope, with no TODO.
- `PROMPT_COPILOT.md`: first and repeat audit prompts.
- `README.md`: this guide.

## Read-only guarantees and limitations
The agent declares only `search` and `read` tools, without editing or terminal tools. Supported tool identifiers and behavior depend on Copilot host/version; verify the agent loads correctly and its available tools before using it. Prompt instructions are not a security boundary. For **hard** protection, run Copilot against a read-only clone/snapshot or OS-level read-only mount, with no write-capable integrations. Also check whether inherited tools or host-specific features expose writes.

No tests are executed by this agent. Test/coverage/lint/format results can be obtained in a separate isolated CI job or by a human, then pasted into Copilot for analysis. Test tools may create cache, coverage or database artifacts. Do not run them on production or shared services.

## Suggested review cycle
1. Run first audit; preserve the full chat report (or copy it to your own notes outside the auditor).
2. Approve findings for a **different** correction agent, which changes code and tests.
3. Have an isolated CI runner execute relevant tests, line/branch coverage, Ruff, Django checks and type checks using the project's configured commands.
4. Run the follow-up audit prompt, supply prior report and CI outputs; demand evidence for resolved findings and identify new regressions.
5. Repeat until no blocking defects remain and relevant quality gates pass; 100% coverage alone is not a guarantee of correctness.

## No human-review workflow
This version intentionally has **no** `HUMAN_REVIEW.md`, no reconciliation requirements and no human-review input dependency.

## When updating from previous archive
Delete the old `docs/ai-review/HUMAN_REVIEW.md` **only if you intentionally no longer need it**. If old `.github/copilot-instructions.md` or `.github/instructions/python-quality.instructions.md` were installed from the previous archive, review them manually; this ZIP does not remove them. Remove any obsolete human-review references from previously merged instructions. Do not blindly overwrite existing project configuration.
