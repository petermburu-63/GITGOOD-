# Portfolio Roadmap

This document tracks three security projects in planning or early development. They are part of the wider GITGOOD portfolio; their implementation code is not currently included in this repository. Progress should be marked complete only after the work is implemented, tested, and documented.

## 1. Secure Boot Certificate Auditor

**Planned stack:** PowerShell and HTML  
**Status:** Planning / early build

A read-only Windows auditing tool to make Secure Boot certificate state easier to inspect. It is intended to parse EFI signature-list data from firmware variables, report whether selected certificate generations are present, check Secure Boot, TPM, and BitLocker status, and produce JSON and a standalone HTML report.

### Planned milestones

- Parse EFI signature lists returned by `Get-SecureBootUEFI`.
- Identify the relevant 2011 and 2023 certificates in `db` and `KEK`.
- Report Secure Boot, TPM, and BitLocker state with clear unsupported/error handling.
- Add a documented green / amber / red verdict and machine-readable JSON output.
- Generate a standalone HTML report.
- Test on the author's own HP EliteBook 835 G8 and document limitations and findings.
- Investigate whether HP BIOS tooling exposes useful related settings.
- Verify any Windows servicing registry keys against current Microsoft documentation before relying on them.

**Planned usage (subject to change):**

```powershell
# Run from an elevated PowerShell session if required to read firmware variables.
.\Invoke-SecureBootAudit.ps1 -OutputPath .\report
```

The script name and parameters are not final. The tool is intended to be read-only and must not modify firmware variables. Certificate lifecycle dates and servicing guidance should be checked against current Microsoft documentation as implementation proceeds.

## 2. Detection-as-Code Lab

**Planned stack:** Sysmon, Sigma, Atomic Red Team, and GitHub Actions  
**Status:** Planning / early build

A controlled lab for practicing detection engineering as a software workflow: generate test telemetry in an isolated Windows VM, write and review Sigma rules, validate them against appropriate event data, and document false positives and tuning decisions.

### Planned workflow

```text
Isolated Windows VM + Sysmon -> event logs -> Sigma rules -> offline validation
                                      ^                  |
                                      |                  v
                              authorized lab tests   CI lint and tests
```

### Planned milestones

- Build an isolated Windows VM and configure Sysmon with a documented baseline.
- Run authorized Atomic Red Team tests only inside that lab.
- Write an initial set of original Sigma rules and map each to MITRE ATT&CK.
- Validate rules against public, appropriately licensed event samples.
- Add CI validation for rule syntax and tests.
- Document each rule's logic, expected telemetry, false positives, tuning, and limitations.
- Expand the rule set based on test results.

**Safety boundary:** Keep simulations in a disposable, isolated VM without access to personal data or the home network. Do not run tests on systems without authorization. Avoid committing sensitive or unlicensed event data.

**Planned layout:**

```text
detection-lab/
├── rules/             # Sigma rules
├── sysmon/            # Sysmon configuration
├── tests/             # Test definitions and approved sample references
├── docs/              # Per-rule notes and tuning decisions
└── .github/workflows/ # CI validation
```

## 3. M-Pesa Smishing Analyzer

**Planned stack:** Python, rules / lightweight ML, and React  
**Status:** Planning / early build

A locally relevant analyzer for identifying potentially suspicious mobile-money SMS messages, including fake reversal, wrong-recipient, and fraudulent loan-link patterns. The goal is to provide an understandable explanation of risk indicators, not to make definitive claims about a sender or message.

### Planned milestones

- Define a labeling scheme and dataset format.
- Collect an initial sample set only with a lawful basis; anonymize it before it enters the repository.
- Implement a transparent rule-based baseline.
- Evaluate with precision and recall, and document dataset limitations.
- Compare the rules with a simple ML baseline.
- Build a small React interface for pasted text and explainable risk indicators.
- Publish dataset documentation and handling procedures.

**Data ethics:** Do not store or publish real phone numbers, names, transaction codes, or other personal data. Minimize collection, anonymize before repository inclusion, and follow applicable privacy requirements, including Kenya's Data Protection Act, 2019. Treat scores as decision support; do not present them as certainty.

## Portfolio context

The author's stated interests include detection engineering, hardware and firmware security, and practical tools for local problems. The Secure Boot auditor is associated with [Hardware-Auditing-HQ](https://github.com/petermburu-63/Hardware-Auditing-HQ); this roadmap keeps the project summaries together while the implementation status remains explicit.

## Keeping this roadmap accurate

Update milestone checkboxes only when work is implemented and tested. Link to code, test evidence, and documentation where available; distinguish planned features from working features and record known limitations.
