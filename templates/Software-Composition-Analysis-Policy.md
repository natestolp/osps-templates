# Software Composition Analysis (SCA) Policy

| This draft policy is inspired by the Open Source Project Security Baseline requirements [OSPS-VM-05.01, OSPS-VM-05.02, OSPS-VM-05.03](https://baseline.openssf.org/versions/2026-02-19.html#osps-vm-05---publish-and-enforce-a-dependency-remediation-policy) |
| :---- |
| Suggested location: SECURITY.md (Dependency Security section) or docs/policies/sca-policy.md, linked from [SECURITY.md](http://SECURITY.md) |
| The SCA tool referenced in this policy must be integrated into the project's CI workflow. Merely documenting an SCA process without enforcing it through the required CI checks does not satisfy OSPS-VM-05.03. |
| Before publishing this policy, the project must replace all placeholders with project-specific values, including: The SCA tool used by the project. The scan schedule. Remediation windows for each severity level. The list of allowed dependency licenses. Licenses requiring maintainer review. Disallowed licenses. The required CI checks and their merge-blocking behavior. |

## Purpose

This policy defines how the project identifies, prioritizes, and remediates Software Composition Analysis (SCA) findings in its dependencies, including known vulnerabilities and license violations. It establishes remediation requirements, requires applicable findings to be resolved before release, and defines the automated enforcement mechanism used to evaluate changes.

## Policy

### 1\. Identification, Prioritization, and Remediation (OSPS-VM-05.01)

#### **Identification**

Project dependencies are scanned for known vulnerabilities and license issues using \[SCA tool name, e.g., OSV-Scanner, Trivy, Dependabot, or Snyk\].

SCA scans run:

* On every pull request.  
* On every change to the default branch.  
* On a scheduled \[daily/weekly\] scan of the default branch to identify newly disclosed vulnerabilities in dependencies that have already been merged.

The SCA process evaluates both direct and transitive dependencies.

#### **Prioritization**

Findings are prioritized in the following order:

1. Severity based on the CVSS base score.  
2. Whether the vulnerable code path is reachable or exercised by the project, when the tooling provides reachability analysis.  
3. Whether a fix is available from the upstream dependency.

#### **Vulnerability Remediation Thresholds**

Vulnerabilities must be remediated by upgrading, patching, replacing, or applying a documented mitigation within the following timeframes:

| Severity | CVSS Score | Remediation Window |
| :---- | :---- | :---- |
| Critical | 9.0 or higher | \[N\] days |
| High | 7.0 to 8.9 | \[N\] days |
| Medium | 4.0 to 6.9 | \[N\] days |
| Low | Below 4.0 | \[N\] days |

Remediation deadlines begin when the finding is identified by the project's SCA process.

#### **License Requirements**

The project maintains an explicit dependency license policy:

* Allowed: \[e.g., MIT, Apache-2.0, BSD-2-Clause, BSD-3-Clause, ISC\]  
* Requires maintainer review before use: \[e.g., LGPL, MPL-2.0\]  
* Disallowed: \[e.g., GPL-3.0 for a permissively licensed project, AGPL-3.0, or any non-OSI/FSF-approved or unlicensed dependency\]

A dependency with a disallowed license is a merge-blocking violation. It must be replaced or have an approved exception documented before the dependency can be merged.

A dependency requiring maintainer review must be reviewed and approved within \[N\] days of identification. The review must document why the dependency is acceptable for the project.

### 2\. Pre-Release Security Gate (OSPS-VM-05.02)

Before publishing any tagged release, the project performs a full SCA scan against the release commit.

The release cannot be published while any of the following remain unresolved:

* Critical vulnerabilities.  
* High vulnerabilities.  
* Disallowed license violations.  
* Other license violations covered by the project's dependency license policy.

A finding may be considered resolved through remediation or an explicitly approved suppression when the finding has been determined to be non-exploitable in the project's context.

The completed SCA check and any approved exceptions are recorded as part of the release checklist.

### 3\. Automated Enforcement (OSPS-VM-05.03)

The project's SCA tool is integrated into the required CI checks and automatically evaluates every pull request and every change to the default branch.

The SCA checks must identify:

* Known vulnerabilities in direct dependencies.  
* Known vulnerabilities in transitive dependencies.  
* Known-malicious packages, including known typosquats and compromised releases.  
* Dependency license violations covered by the project's license policy.

A merge-blocking status check fails when a finding exceeds the remediation thresholds defined in Section 1 or violates the dependency license policy.

### 4\. Exceptions and Suppressions

A finding may be suppressed only when there is sufficient evidence that it is not exploitable or otherwise does not apply to the project.

Every suppression must include:

* The affected dependency and finding.  
* The reason the finding does not apply or is not exploitable.  
* Any relevant technical evidence or analysis.  
* The date of the decision.  
* An assigned maintainer responsible for reviewing the exception.

Exceptions must be approved by a maintainer who is not the author of the pull request introducing or modifying the affected dependency.

Where supported by the SCA tooling, exceptions should be recorded using a VEX statement or an equivalent machine-readable suppression mechanism.

Exceptions must be reviewed periodically and removed when they are no longer justified.
