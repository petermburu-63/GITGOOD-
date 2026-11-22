# GITGOOD  Security Engineering Labs

A Python learning portfolio for exploring security engineering through small, documented lab exercises. The repository emphasizes understanding, evidence, and defensive thinking—not unauthorized testing.

> **Authorized use only:** Run network-facing exercises only in a lab you own or have explicit written permission to assess. Review each script's documentation and scope before running it.

## What you'll find as u go....

| Area | Focus | Examples |
| --- | --- | --- |
| `offense/` | Controlled discovery and security concepts | Port scanning, packet inspection, hash exercises, vulnerability lookups |
| `defense/` | Host monitoring and defensive workflows | Host monitoring |
| `analytics/` | Interpreting security telemetry | Telemetry analysis |
| `docs/` | Lab context and responsible-use guidance | Security lab guide |

## Repository layout

```text
.
├── LICENSE
├── README.md
└── cybersecurity-projects/
    ├── README.md
    ├── requirements.txt
    ├── analytics/
    │   └── telemetry_analyzer.py
    ├── defense/
    │   └── host_monitor.py
    ├── offense/
    │   ├── 01_port_scanner.py
    │   ├── 02_packet_sniffer.py
    │   ├── 03_hash_cracker.py
    │   ├── 08_vuln_scanner.py
    │   ├── advanced_recon_suite.py
    │   └── README.md
    └── docs/
        └── SECURITY_LAB_GUIDE.md
```

The `offense/` directory contains the current discovery-focused exercises; the project README documents their intended scope and learning flow.

## Getting started

Use Python 3 and create an isolated environment from the repository root:

```bash
python3 -m venv .venv
source .venv/bin/activate  # Windows: .venv\\Scripts\\activate
python -m pip install --upgrade pip
python -m pip install -r cybersecurity-projects/requirements.txt
```

PLS PLS PLS I SAY AGAIN PLS -------Before using an exercise, read its source and the relevant documentation. Start with a disposable, isolated lab and data that you are authorized to inspect. Dependencies and system permissions may vary by exercise and platform---------------.

## Learning path

1. Read the project and safety guides.
2. Learn discovery concepts in a controlled lab.
3. Compare observations with defensive monitoring and telemetry.
4. Record limitations, evidence, and responsible remediation ideas.

## Project principles

- **Permission first:** Never target systems without explicit authorization.
- **Small and explainable:** Prefer readable exercises with clear inputs and limitations.
- **Evidence over assumptions:** Distinguish observed facts from interpretation.
- **Defensive learning:** Use findings to understand risk and improve protection.

## Portfolio roadmap

The [portfolio roadmap](docs/PORTFOLIO_ROADMAP.md) describes three related projects currently in planning or early development: a read-only Secure Boot certificate auditor, an isolated detection-as-code lab, and a privacy-conscious M-Pesa smishing analyzer. These are roadmap items, not claims that their implementations are already included in this repository.

## Contributing

Keep contributions focused and reproducible. Include the purpose, safe test conditions, dependencies, expected output, limitations, and documentation for any new exercise. Do not include real credentials, personal data, or sensitive network captures.

## License

See [LICENSE](LICENSE) for license terms.
