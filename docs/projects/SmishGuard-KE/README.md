# SmishGuard-KE

> **Work in progress · v0.1.0** — An explainable, rule-based SMS-fraud scoring project focused on Kenyan mobile-money-style scam patterns. The supplied project brief describes a standard-library-only Python implementation.

This document is a project brief in GITGOOD. It is not the analyzer source code or dataset. Status and test claims below are reported by the author and have not been independently verified in this repository.

## Context

Smishing (SMS phishing) can use locally familiar social-engineering stories: a fake mobile-money confirmation followed by a request to return a mistaken transfer, fraudulent refund links, or loan and Fuliza offers that ask for an upfront fee. Messages may combine English, Kiswahili, and Sheng.

The planned analyzer scores messages from 0 to 100 and returns named reasons with evidence, rather than presenting a black-box decision.

## Signals described in the project brief

| Signal | Example / notes | Starting weight |
| --- | --- | ---: |
| PIN, OTP, or password request | Requests for credentials | 45 |
| Confirmation-style text from a non-`MPESA` sender | Sender-aware; needs sender input | 45 |
| Brand-lookalike link | Brand in URL but not an approved domain | 35 |
| Wrong-transfer story | e.g. “nimetuma kimakosa” | 30 |
| Advance-fee request | e.g. processing fee / registration fee | 30 |
| Prize or lottery lure | Prize language | 25 |
| Account-suspension or KYC lure | Threat / action pressure | 25 |
| IP-literal URL | URL uses an IP address | 25 |
| Brand mention from ordinary phone number | Context-dependent | 25 |
| Loan / Fuliza limit lure | Often paired with a fee request | 20 |
| Odd transaction-code length | Format heuristic | 20 |
| Shortener, punycode, unusual TLD, plain HTTP | URL indicators; weights vary | 20 / 15 / 10 / 5 |
| Urgency / job / easy-money lure | Context-dependent wording | 15 / 10 |
| Standard-format message from expected sender | Weak negative signal only | -10 |

Weights are hand-selected starting values, not learned. The supplied brief reports configurable labels: `likely_scam` at 60+, `suspicious` at 30+, otherwise `low_risk`. Scores are indicators for review, not proof.

## Interface described by the project

The supplied project README describes a Python package and CLI with `analyze`, `batch`, and `eval` commands, plus a possible React interface. The example below is illustrative and should be checked against the actual source project's current CLI:

```bash
smishguard analyze "Reply with your PIN and OTP" --json
smishguard batch data/samples_synthetic.csv --out results.csv
smishguard eval data/samples_synthetic.csv
```

As a library, the reported interface is `from smishguard import analyze`. Check the source project's documentation for the current API and options.

## Design goals

- **Explainability:** Return named indicators and evidence for each score contribution.
- **Privacy:** Mask phone numbers before rendering evidence snippets; avoid storing or publishing personal messages.
- **Sender-aware analysis:** Use sender information where provided, and state when it is absent.
- **Low setup burden:** The supplied brief describes a standard-library-only implementation.

## Status reported by the author

The supplied project README reports a rule lexicon for English, Kiswahili, and some Sheng; URL, sender, and transaction-code heuristics; a CLI and Python API; 13 unit tests; and CI for Python 3.9 and 3.12. It reports that tests passed locally on Python 3.12. These claims have not been independently verified in this repository.

The bundled 24-row dataset is described as synthetic and suitable only as a smoke test, not as evidence of real-world accuracy. The author notes that some synthetic scams fall below the default `likely_scam` threshold.

Planned work includes a consented, anonymized dataset, comparison with a simple learned baseline, a broader community-reviewed lexicon, verification of the official-domain allowlist, and an optional client-side web demo.

## Limitations and responsible use

- Heuristics can produce false positives and false negatives; wording and scam tactics change.
- Sender IDs can be spoofed. A familiar sender or a lower score does not prove a message is legitimate.
- Transaction-code length and URL allowlists are format-dependent heuristics; verify them before relying on them.
- Never share a PIN or OTP because a message requests it. No score replaces checking through an official channel.
- Do not use the lexicon to craft scams, or scrape, store, or publish real people's messages or phone numbers. Collect data only with a lawful basis, minimize it, and anonymize it before repository inclusion.
- Follow applicable privacy requirements, including Kenya's Data Protection Act, 2019.

## License and author

The supplied project brief states MIT; check the source project for its license file.  
Peter M. Mburu — IT & Cybersecurity student, Kenya.
