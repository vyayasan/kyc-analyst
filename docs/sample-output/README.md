# Sample Output — What the Plugin Produces

These are sanitized examples of actual plugin output. Customer details are fictional. The report structure, search methodology, risk scoring, and stagegate flow are exactly what the plugin produces in a real onboarding workflow.

## Files

| File | Description |
|------|------------|
| [SAMPLE-Step0-Report.md](./SAMPLE-Step0-Report.md) | Full Step 0 Verification Report — 9 sections covering customer profile, all 6 search results, discrepancy register, risk scoring calculation, escalation trigger check, decision, and compliance certification |
| [SAMPLE-Audit-Trail.txt](./SAMPLE-Audit-Trail.txt) | Immutable audit trail showing all 17 stagegates with timestamps, actors, consent keywords, and evidence references |

## What a real run also produces (not included here)

- **4-sheet Excel dashboard** (.xlsx) — Executive Summary, Directorships, Discrepancies, Risk Assessment sheets with formatted tables
- **PDF report** (.pdf) — 6-page formatted report with the same content as the markdown report, styled with headers, tables, and compliance certification
- **Case folder** — Numbered directory structure (001-006) containing all evidence files, search results, metadata, and the locked audit trail

## Case folder structure

```
KYC-20260215-ONB-SMITH-001/
├── 001_CASE_METADATA/
│   └── CASE_METADATA.md
├── 002_STEP_0_SEARCHES/
│   ├── Search_1_Findings.md        (Adverse Media)
│   ├── Search_1.5_Findings.md      (ICIJ Offshore Leaks)
│   ├── Search_2_Findings.md        (Directorships)
│   ├── Search_3_Findings.md        (PEP Status)
│   ├── Search_4_Findings.md        (Professional Background)
│   ├── Search_5_Findings.md        (Sanctions/Crime)
│   └── STEP_0_VERIFICATION_REPORT.md
├── 003_VERIFICATION_OUTCOMES/
├── 004_DECISION_DOCUMENTATION/
├── 005_ESCALATION_BRIEF/           (created only if escalation triggered)
└── 006_AUDIT_TRAIL/
    └── AUDIT_TRAIL.md              (immutable — locked after case finalization)
```
