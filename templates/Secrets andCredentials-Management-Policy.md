# Secrets and Credentials Management Policy

> This draft policy is inspired by the Open Source Project Security Baseline requirement OSPS-BR-07.02.

> **Suggested location:** `SECURITY.md` (Secrets Management section) or `docs/policies/secrets-management.md`, linked from `SECURITY.md`.

The project's secrets and credentials management process must define how secrets are protected from disclosure through the version control system and CI/CD workflows.

Before publishing this policy, the project must replace all placeholders with project-specific values, including:

- The secret storage mechanism used by the project.
- The secret-scanning tool or mechanism used by the project.
- The files and credential patterns excluded from version control.
- The maintainers or roles authorized to access stored secrets.
- The credential rotation schedule.
- The process for responding to suspected credential compromise.
- The process for handling secrets accidentally committed to the repository.

## Purpose

This policy defines how the project stores, accesses, protects, and rotates secrets and credentials, including API keys, tokens, private keys, service account credentials, and other sensitive authentication data. It establishes controls to prevent the unintentional disclosure of secrets through the project's version control system and CI/CD workflows.

## Policy

### 1. Secret Storage and Protection

Secrets and credentials MUST NOT be committed to the project's version control system in plaintext, including in branches, tags, commit history, test fixtures, or example configuration files.

Secrets required by CI/CD workflows are stored using the project's designated encrypted secrets store:

**Secret storage mechanism:** [encrypted secrets store]

Examples include GitHub Actions Encrypted Secrets or GitLab CI/CD Variables configured as protected and masked.

The project maintains version-control exclusion rules for common credential files and patterns, including:

- `.env`
- `*.pem`
- `*.key`
- `id_rsa*`
- [project-specific credential files or patterns]

### 2. Secret Detection

The project uses [secret-scanning tool or mechanism, e.g., Gitleaks, TruffleHog, or the version control platform's built-in scanner] to detect secrets and credentials in the project's source code and repository history.

Secret scanning runs:

- On every pull request.
- On every push to the default branch.
- On a scheduled [daily/weekly] scan.

A detected secret is handled according to the incident response process defined in Section 5.

### 3. Access Control

Secrets are scoped to the minimum set of workflows, jobs, environments, or services that require access.

Organization-wide secrets are avoided where repository- or environment-scoped secrets provide sufficient access.

Access to view or modify stored secrets is limited to:

**Authorized roles:** [project maintainers / security team / specific project roles]

### 4. Credential Rotation

Long-lived credentials are rotated according to the following schedule:

| Credential Type | Rotation Schedule |
|---|---|
| Service account credentials | [N] days |
| Personal access tokens | [N] days |
| Signing keys | [N] days |
| Other long-lived credentials | [N] days |

Credentials are revoked or rotated immediately when compromise is suspected, including following:

- Accidental exposure in the repository.
- Offboarding of a maintainer with access to the credential.
- A security incident affecting the credential.
- A dependency or vendor breach that may affect the credential.

### 5. Secret Exposure and Incident Handling

Any secret discovered in the project's repository is treated as compromised.

The exposed credential MUST be revoked or rotated immediately, regardless of whether the exposed content is subsequently removed from the repository history.

The project records and handles the exposure according to its [incident response process / coordinated vulnerability disclosure policy], where applicable.

Repository history may be scrubbed to remove the exposed credential, but history removal does not replace credential revocation or rotation.

### 6. Policy Review

This policy is reviewed according to the following schedule:

**Review cadence:** [e.g., annually]

The policy is also reviewed following a significant secret-exposure incident or a material change to the project's secret storage, CI/CD, or access-control mechanisms.
