# Escalated Permissions Review Policy

> This draft policy is inspired by the Open Source Project Security Baseline requirement OSPS-GV-04.01.

> **Suggested location:** `GOVERNANCE.md` or `MAINTAINERS.md`

Before granting escalated permissions to project resources, the project must define and follow a documented review process for evaluating collaborators who are being granted those permissions.

Before publishing this policy, the project must replace all placeholders with project-specific values, including:

- The resources and permissions considered escalated.
- The minimum contribution history required for eligibility.
- The timeframe over which contributions are evaluated.
- The maintainer or role responsible for nomination.
- The identity-verification process.
- The required approval process.
- The access-review cadence.
- The conditions that require access to be reduced or revoked.

## Purpose

This policy defines how collaborators are reviewed and vetted before being granted escalated permissions to sensitive project resources. It establishes eligibility, identity verification, approval, periodic review, and revocation processes to reduce the risk of unauthorized access or misuse.

## Scope

For this policy, escalated permissions include:

- Write or merge access to the primary branch.
- Administrative access to the repository or organization.
- Access to CI/CD secrets.
- Release or publishing rights, including package registries, container registries, or signing keys.

## Policy

### 1. Eligibility and Nomination

A collaborator is eligible for escalated permissions only after demonstrating a documented and sustained contribution history.

**Minimum contribution requirement:** [e.g., 5 merged pull requests over 3 months]

The collaborator must be nominated by an existing maintainer who already has the requested level of escalated access.

### 2. Identity Verification

Before escalated permissions are granted, at least one existing maintainer verifies that the nominee's identity is consistent with their established project participation.

The verification may include:

- Reviewing the nominee's established version control account history.
- Confirming consistent participation under the same identity.
- Confirming claimed organizational affiliation when relevant to the project's threat model.

**Identity verification process:** [project-specific process]

### 3. Approval

Granting escalated permissions requires explicit, documented approval from at least one maintainer other than the nominee.

Approval may be recorded through:

- A governance issue.
- Meeting records.
- A pull request updating `MAINTAINERS.md`.
- [Other project-specific mechanism.]

A collaborator MUST NOT approve their own permission escalation.

### 4. Access Review

Existing escalated permissions are reviewed according to the following schedule:

**Review cadence:** [e.g., annually]

Access is also reviewed when a maintainer becomes inactive for [N] days/months or no longer requires the permission for their role.

Permissions that are no longer required are reduced to the lowest level of access consistent with the maintainer's continued participation.

### 5. Permission Revocation

Escalated permissions are revoked when:

- A maintainer voluntarily steps down.
- A maintainer is removed through the project's governance process.
- The permission is no longer required for the maintainer's role.
- [Other project-specific revocation condition.]

Revocation is performed promptly after the applicable condition is identified.
