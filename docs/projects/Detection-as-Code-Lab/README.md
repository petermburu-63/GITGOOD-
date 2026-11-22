# Detection-as-Code Lab

> **Project brief · Work in progress · v0.1.0**

A small detection-engineering lab for treating Sigma rules as maintainable software: lint metadata, test rules against labelled events, and run checks in CI.

This brief summarizes the project information supplied by the author. The Detection-as-Code Lab implementation is not included in this repository; verify implementation and test status in its source project before relying on these claims.

## Approach

Each detection is intended to be:

1. Written as a vendor-neutral Sigma rule.
2. Checked for required metadata, valid UUIDs, MITRE ATT&CK tags, and documented false positives.
3. Tested against labelled true-positive and false-positive events.
4. Gated by CI so broken or untested rules are caught during review.

## Reported starter rules

| Rule | ATT&CK | Level | Reported labelled tests |
| --- | --- | --- | --- |
| Suspicious Process Access to LSASS Memory | T1003.001 | Medium | 2 TP / 3 FP |
| PowerShell Launched With Encoded Command | T1059.001, T1027 | Medium | 2 TP / 3 FP |
| Certutil Used To Fetch Content From A URL | T1105 | High | 2 TP / 2 FP |
| New Service Installed With Suspicious Image Path | T1543.003 | Medium | 2 TP / 2 FP |

See the source project's `docs/ATTACK-COVERAGE.md` for rule details when available.

## Intended layout

```text
rules/                   Sigma rules (*.yml)
tests/events/<rule>/     Labelled positive and negative JSON events
tests/test_minisigma.py  Evaluator unit tests
tools/minisigma.py       Limited Sigma-subset evaluator
tools/validate_rules.py  Metadata linter
tools/run_tests.py       Rule/event test runner
docs/                    ATT&CK mapping, lab guide, tuning notes
.github/workflows/       CI
```

## Local workflow

The commands below describe the supplied project brief and assume they are run from the Detection-as-Code Lab source directory:

```bash
python -m venv .venv
source .venv/bin/activate  # Windows: .venv\\Scripts\\activate
pip install -r requirements.txt

python tools/validate_rules.py
python -m unittest tests/test_minisigma.py
python tools/run_tests.py
```

## Evaluator scope

The reported `tools/minisigma.py` implementation supports only a limited subset of Sigma syntax, including selected field modifiers and boolean conditions. It is not a Sigma compiler. Use a maintained Sigma conversion tool or a supported hunting platform for broader compatibility, and verify current command syntax in that tool's documentation. Unsupported constructs should fail clearly rather than be treated as passing detections.

## Status reported by the author

The supplied project README reports four starter rules, a metadata validator, labelled-event runner, evaluator tests, a GitHub Actions workflow, ATT&CK documentation, and passing local tests on Python 3.12. These results have not been independently run or verified in this repository.

The brief also reports that the isolated Sysmon / Atomic Red Team VM workflow and real-telemetry tuning are not yet complete. Planned work includes validating with pySigma or sigma-cli, testing against appropriately licensed public EVTX samples, adding rules, and exporting through pySigma backends.

## Safety and limitations

- Run simulations only in an isolated lab you own or are explicitly authorized to use. Snapshot the VM, review tests before execution, and follow their cleanup instructions.
- Starter rules are examples, not production detections. Noisy behavior, telemetry configuration, and environment-specific field names affect results.
- Handwritten test events exercise rule logic; they do not establish real-world detection coverage.
- Do not commit sensitive event data or samples without permission and appropriate licensing.

## License and author

The supplied project brief states MIT; check the source project for its license file.  
Peter M. Mburu
