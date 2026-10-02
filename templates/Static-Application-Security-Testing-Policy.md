# Static Application Security Testing (SAST) Policy

> This draft policy is inspired by the Open Source Project Security Baseline requirements OSPS-VM-06.01 and OSPS-VM-06.02.

> **Suggested location:** `SECURITY.md`

> **Implementation requirement:** The SAST tool referenced in this policy must be integrated into the project's CI workflow. Merely documenting a SAST process without enforcing it through the required CI checks does not satisfy OSPS-VM-06.02.

Before publishing this policy, the project must replace all placeholders with project-specific values, including:

- The SAST tool used by the project.
- The scan schedule and events that trigger scans.
- Remediation windows for each severity level.
- The severity threshold that blocks a change from being merged.
- The required CI checks and their merge-blocking behavior.
- The approved process for suppressing or excepting SAST findings.

## Purpose

This policy defines how the project identifies, prioritizes, and remediates static-analysis findings in its own codebase. It establishes remediation requirements and defines the automated enforcement mechanism used to evaluate changes against those requirements.

## Policy

### 1. Identification, Prioritization, and Remediation (OSPS-VM-06.01)

#### Identification

The project's source code is scanned for security vulnerabilities using [SAST tool name, e.g., CodeQL, Semgrep, gosec, or Bandit].

SAST scans run:

- On every pull request.
- On every change to the default branch.
- On a scheduled [daily/weekly] scan of the default branch to identify newly detected issues in code that has already been merged.

The SAST process analyzes the project's own source code and reports security findings according to the rules and severity classifications configured for the project.

#### Prioritization

Findings are prioritized according to:

1. Severity assigned by the SAST tool.
2. The potential security impact of the finding.
3. Whether the vulnerable code path is reachable or exploitable in the project's context, when this can be determined.

#### Remediation Thresholds

SAST findings must be remediated by fixing the affected code or applying a documented mitigation within the following timeframes:

| Severity | Remediation Window |
|---|---|
| Critical | [N] days |
| High | [N] days |
| Medium | [N] days |
| Low / Informational | [N] days or tracked in the project backlog |

Remediation deadlines begin when the finding is identified by the project's SAST process.

### 2. Automated Enforcement (OSPS-VM-06.02)

The project's SAST tool is integrated into the required CI checks and automatically evaluates changes to the project's codebase.

The SAST check runs:

- On every pull request.
- On every change to the default branch.
- [Any additional project-specific trigger.]

A merge-blocking status check fails when a finding meets or exceeds the severity threshold defined by the project's SAST policy.

**Merge-blocking threshold:** [Critical / High / Critical and High / other project-specific threshold]

A change that introduces a finding at or above the merge-blocking threshold MUST NOT be merged unless the finding is resolved or an approved exception is recorded according to Section 3.

### 3. Exceptions and Suppressions

A SAST finding may be suppressed only when there is sufficient evidence that the finding is a false positive, non-exploitable, or otherwise does not apply to the project's context.

Every suppression must include:

- The affected source code and finding.
- The reason the finding does not apply or is not exploitable.
- Any relevant technical evidence or analysis.
- The date of the decision.
- An assigned maintainer responsible for reviewing the exception.

Exceptions must be approved by a maintainer who is not the author of the pull request introducing or modifying the affected code.

Where supported by the SAST tooling, exceptions should be recorded using the tool's native suppression mechanism or an equivalent tracked exception.

Exceptions must be reviewed periodically and removed when they are no longer justified.
