# Test Coverage Policy

> This draft policy is inspired by the Open Source Project Security Baseline requirement OSPS-QA-06.03.

> **Suggested location:** `CONTRIBUTING.md` (Testing section) or `docs/policies/test-coverage-policy.md`, linked from `CONTRIBUTING.md`.

> **Implementation requirement:** The project must require automated tests for major changes to the project's software. Merely having a general test suite or recommending that contributors add tests does not satisfy OSPS-QA-06.03.

Before publishing this policy, the project must replace all placeholders with project-specific values, including:

- The criteria used to identify a major change.
- The project's automated test suite or testing framework.
- The types of automated tests expected for major changes.
- The process used to verify that major changes include corresponding tests.
- The process for handling exceptions.

## Purpose

This policy defines what constitutes a major change to the project's software and establishes the testing requirements for those changes. It ensures that major changes are accompanied by automated tests that exercise the changed behavior and help prevent functional and security regressions.

## Policy

### 1. Definition of a Major Change (OSPS-QA-06.03)

A major change is any pull request that:

- Adds a new feature.
- Changes existing externally visible behavior, such as CLI flags, API behavior, or output formats.
- Fixes a functional or security bug.
- Modifies security-relevant logic, such as authentication, input validation, or permission checks.

The following changes are not considered major changes:

- Documentation-only changes.
- Formatting-only changes.
- Refactoring that does not change externally visible behavior.

### 2. Automated Test Requirements (OSPS-QA-06.03)

Every major change must add new automated test(s) or update existing automated test(s) in the project's automated test suite.

The tests must exercise the behavior changed by the pull request.

Bug fixes must include regression tests that demonstrate the corrected behavior where the behavior can be tested through the project's automated test suite.

### 3. Test Verification

Test coverage for major changes is verified as part of pull request review.

Reviewers verify that:

- The change meets the project's definition of a major change.
- Corresponding automated tests have been added or updated.
- The tests exercise the changed behavior.
- Regression tests are included for applicable bug fixes.

The project may use CI coverage tooling to identify changes in test coverage, but coverage tooling is not required unless separately specified by the project.

### 4. Exceptions

An exception may be granted when a major change cannot reasonably be tested using the project's existing automated test infrastructure.

Each exception must include:

- A description of why the change cannot currently be tested.
- Approval from a project maintainer.
- A tracked follow-up issue describing the required test coverage.
- The expected timeframe for adding the missing coverage, where applicable.
