# Changelog

All notable changes to the KYC Analyst plugin are documented here.

Format follows [Keep a Changelog](https://keepachangelog.com/en/1.1.0/). This project uses [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [1.0.0] - 2026-02-15 — First Public Release

First open-source release of the KYC Analyst plugin for Claude Cowork.

### Features

- **Step 0 Independent Verification** — 6 mandatory search categories (Adverse Media, ICIJ Offshore Leaks, Directorships, PEP, Professional Background, Sanctions) across 90+ sources, executed before any due diligence begins
- **17 Mandatory Stagegates** — Human-in-the-loop enforcement at every decision point. No auto-approvals, no skipping, no proceeding on silence
- **Deterministic Risk Scoring** — Four-factor weighted model (Geographic 30%, Customer 35%, Product 25%, Channel 10%) with published formulas. Same inputs always produce the same score
- **6 Slash Commands** — `/kyc:onboard`, `/kyc:onboard-interactive`, `/kyc:screen`, `/kyc:risk`, `/kyc:monitor`, `/kyc:refresh`
- **Interactive Onboarding Mode** — Step-by-step dialog guidance for new analysts
- **Excel Dashboard** — 4-sheet workbook (Executive Summary, Directorships, Discrepancies, Risk Assessment) via openpyxl
- **PDF Report** — 17-section professional compliance report via fpdf2
- **Case Folder Management** — Auto-created numbered folder structure (001-006) with immutable audit trail
- **5 Workflow Templates** — Copy-paste ready for Individual, HNWI, SME, Complex Corporate, and Refresh cases
- **5 Worked Examples** — Complete input/output examples with expected results
- **MCP Integration** — Claude in Chrome (browser automation), fpdf2 (PDF), openpyxl (Excel) with tool-agnostic `~~placeholder` connector system
- **Multi-jurisdiction Support** — UK/EU (AMLD5, MLR 2017, FCA), US (FinCEN, BSA/AML, OFAC), MENA (CBUAE, SAMA)
- **Connector Flexibility** — Tool-agnostic `~~placeholder` syntax works with Google Drive, Box, Salesforce, Chrome, Slack, and others

### Data Sources

All free and public: OFAC SDN, UN Consolidated List, EU Sanctions List, UK HMT, OpenSanctions PEP (100+ countries), Companies House API, ICIJ Offshore Leaks (Panama/Paradise/Pandora Papers), SEC EDGAR.

### Known Limitations

- fpdf2 does not support Unicode characters (checkmarks) with Helvetica font — uses `[OK]`/`[X]` instead
- fpdf2 requires `new_x="LMARGIN", new_y="NEXT"` syntax (not deprecated `ln=True`)
- Excel cells containing `===` may serialize incorrectly with Desktop Commander — use alternative separators
- Claude Cowork and plugins are in research preview — features and behavior may change
- Only `/kyc:onboard-interactive` has been extensively tested in production pilots. Other commands have been tested in development but not in production compliance environments
