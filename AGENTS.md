# AGENTS.md — Permanent Engineering Baseline

This file is the authoritative operating contract for AI agents and developers working in this repository. Read it before changing code. Project-specific instructions may extend these rules, but must not silently weaken them.

## 1. Operating model: COHI

Use the COHI composed-intelligence model. Core sequence:

`INSPECT → DIAGNOSE → PLAN → ISSUE → BRANCH → IMPLEMENT → TEST → PR → REVIEW → DEPLOY → OBSERVE`

Never use `GUESS → PATCH → DEPLOY`. If something was not verified, state `NOT VERIFIED`. Never fabricate repository state, logs, test results, deploy status, API behavior, dependencies or validation.

## 2. GitHub workflow is mandatory

Every relevant bug fix, improvement, refactor, security/performance/infrastructure change or new feature must have a GitHub Issue before implementation. Work on a dedicated branch. Every change must be delivered through a Pull Request and the PR description must link its Issue, preferably with `Closes #123` or `Fixes #123`.

Deploys must be traceable to approved PRs. Use Conventional Commits and Commitlint when supported.

If GitHub Issues are disabled for the repository, this must be treated as a repository-configuration blocker. Bootstrap changes may be documented in a dedicated PR, but Issues should be enabled before normal development resumes.

## 3. Diagnose before altering

Inspect current implementation, dependencies, configuration and runtime/CI state before modifications. Identify root cause or product requirement, define the smallest safe change, and preserve rollback capability for operational changes.

## 4. UI states, loading and motion

Use `https://github.com/kylezantos/design-motion-principles` as the motion-design reference. Every asynchronous UI must consider relevant states such as idle, loading, success, empty, error, retry, disabled, uploading, processing, queued and syncing when applicable.

Use skeletons when they preserve layout and improve perceived loading. Use lazy loading/code splitting where appropriate. Provide progress feedback for meaningful waits. Use smooth intentional enter/exit/state transitions when they improve orientation. Respect `prefers-reduced-motion` and prioritize mobile performance.

## 5. Observability

Prefer OpenTelemetry as a vendor-neutral instrumentation layer when suitable. Integrate the backend that best fits the project, such as Sentry, Datadog or New Relic. Do not install all vendors solely to satisfy a checklist.

Cover structured logs, exceptions, metrics, traces/spans, latency, database activity, queues/jobs, integrations, authentication failures, runtime errors and release/deploy context. Never log passwords, secrets or access tokens.

## 6. Architecture and code quality

Maintain an explicit architecture/dependency contract for boundaries, responsibilities, dependency direction, data access, tenancy/security boundaries and service interfaces. Automate constraints in CI when practical.

Use tooling according to stack and value: Biome, Commitlint + Conventional Commits, Knip and Stryker mutation testing when appropriate. Do not add redundant tools solely for checklist compliance.

## 7. Testing and CI

Maintain unit, integration and end-to-end tests appropriate to the system. Use Playwright as the preferred web E2E reference when suitable and Codecov when useful for coverage visibility.

PRs should pass applicable gates such as typecheck, lint/format, unit tests, integration tests, E2E, build, Knip, architecture checks, security checks, coverage and mutation testing when configured. Never claim a gate passed unless it actually ran or was reported by CI.

## 8. Performance, security and tenancy

Consider bundle size, rendering, caching, lazy loading, code splitting, images, API latency, database queries/indexes, N+1 risks, CPU/memory and mobile constraints. Preserve least privilege, secret hygiene, input validation, authorization boundaries and tenant isolation.

## 9. Definition of done

A change should be traceable, testable, reviewable, reversible according to risk, observable in production when applicable, and documented where future agents need context.

Issue records the reason. Branch isolates the work. Code implements it. Tests demonstrate behavior. PR records and reviews the change. CI enforces gates. Deployment promotes an approved revision. Observability validates production behavior.
