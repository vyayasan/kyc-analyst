<p align="center">
  <img src="docs/banner.svg" alt="KYC Analyst" width="900"/>
</p>

<p align="center">
  <a href="https://github.com/vyayasan/kyc-analyst/blob/main/LICENSE"><img src="https://img.shields.io/badge/license-MIT-green.svg" alt="MIT License"/></a>
  <a href="https://github.com/vyayasan/kyc-analyst/releases"><img src="https://img.shields.io/badge/version-1.0.0-blue.svg" alt="Version 1.0.0"/></a>
  <a href="https://claude.ai/cowork"><img src="https://img.shields.io/badge/platform-Claude%20Cowork-black.svg" alt="Claude Cowork"/></a>
  <a href="https://www.linkedin.com/in/sandipanee"><img src="https://img.shields.io/badge/-Sandi%20S-blue?logo=linkedin&style=flat-square" alt="LinkedIn"/></a>
  <a href="https://twitter.com/vyayasan"><img src="https://img.shields.io/twitter/follow/vyayasan" alt="Twitter"/></a>
</p>

---

Your compliance team deserves better tools.

Open-source KYC/AML compliance automation for [Claude Cowork](https://claude.ai/cowork). Uses only free public data sources. 17 mandatory human-in-the-loop checkpoints — AI assists, the analyst decides.

> **Note:** Claude Cowork and plugins are currently in research preview. This plugin is an experimental open-source project and should be evaluated accordingly. See [Disclaimer](#disclaimer) below.

**[Demo Slides (PDF)](./docs/demo-slides.pdf)** — 22-page walkthrough of the full onboarding workflow and output samples.

## Quickstart

```bash
git clone https://github.com/vyayasan/kyc-analyst.git
pip install -r requirements.txt
```

Then in Claude Cowork:

```
/kyc:onboard-interactive "Jane Smith" -- UK resident, salaried employee, standard risk
```

See [QUICK_START_GUIDE.md](./QUICK_START_GUIDE.md) for a 10-minute walkthrough, or keep reading for how it works.

---

## Why This Exists

Compliance analysts at small teams spend most of their time on tasks that shouldn't require expensive platforms: navigating public websites, screening free databases, calculating risk scores using published formulas, and writing reports.

The underlying data sources — OFAC, UN, EU sanctions lists, Companies House, OpenSanctions — are all free. The risk formulas (MLR 2017, FinCEN CDD) are publicly documented. The workflows are well-understood.

Yet teams pay tens of thousands per year for platforms that essentially orchestrate access to these free resources.

This plugin does the same orchestration while enforcing 17 mandatory human-in-the-loop checkpoints. No auto-approvals. No skipping. The analyst stays in control of every decision.

## Early Results

> **Caveat:** These are early-stage results from a single pilot. They are not guaranteed, not independently audited, and may not be representative of all compliance environments. Your results will vary depending on case complexity, team experience, jurisdiction, and workflow configuration.

One UK fintech ran this plugin for 30 days with a team of 5 compliance analysts on standard-risk individual onboarding cases:

| Metric | Before | After | Notes |
|--------|--------|-------|-------|
| Time per case | ~95 min | ~27 min | Standard individual cases only |
| Tooling cost | Annual platform subscription | Claude Pro subscription | Does not include analyst time or overhead |
| Legal review | — | Approved for pilot use | Firm-specific legal assessment |

These numbers reflect one team's experience with one type of case. Enhanced due diligence, complex corporate structures, and multi-jurisdiction cases will take longer.

## How It Works

<p align="center">
  <img src="docs/kyc-analyst-workflow.svg" alt="KYC Analyst 17-Stagegate Workflow" width="900"/>
</p>

<p align="center">
  <sub><a href="docs/kyc-analyst-workflow.excalidraw">Open in Excalidraw</a> · Editable source file included in repo</sub>
</p>

```
Customer docs ──> Claude extracts ──> Analyst verifies
                                           │
                                     [STAGEGATE 1-5]
                                           │
Step 0: 6 mandatory searches ────────> Analyst reviews each
  • Adverse media (72+ sources)            │
  • ICIJ Offshore Leaks               [STAGEGATE 6-12]
  • Directorships (Companies House)        │
  • PEP status (5 databases)              │
  • Professional background                │
  • Sanctions (OFAC/UN/EU/UK)              │
                                           ▼
Risk scoring (deterministic) ────────> Analyst approves
  • Geographic  30%                        │
  • Customer    35%              [STAGEGATE 13-14]
  • Product     25%                        │
  • Channel     10%                        ▼
                                     PROCEED or ESCALATE
                                           │
                                     [STAGEGATE 15-17]
                                           │
                                     Excel + PDF + Case Folder
```

Every `[STAGEGATE]` requires explicit analyst consent before proceeding. 17 total. Zero auto-approvals.

### Risk Scoring Model

Deterministic four-factor weighted model. Same inputs always produce the same score. No ML, no black boxes.

| Factor | Weight | Inputs |
|--------|--------|--------|
| Geographic | 30% | Country of residence, nationality, transaction corridors |
| Customer | 35% | Customer type, occupation, source of wealth, PEP status |
| Product | 25% | Product type, transaction limits, delivery channel |
| Channel | 10% | Onboarding method, face-to-face vs remote |

| Band | Score | Action |
|------|-------|--------|
| LOW | 0–20 | Standard CDD |
| MEDIUM | 21–60 | Enhanced monitoring |
| HIGH | 61–80 | Enhanced Due Diligence (EDD) |
| CRITICAL | 81–100 | Senior management review or decline |

### Stagegate Architecture

Stagegates are the enforcement mechanism. Each gate follows a strict pattern:

```
GATE ──> PRESENT evidence ──> WAIT for analyst ──> PROCEED only on explicit consent
```

The plugin will **not** proceed on silence. If the analyst doesn't respond, the workflow pauses indefinitely. This is by design — regulatory compliance requires affirmative human decisions, not timeouts or defaults.

HITL trigger keywords: `ready`, `continue`, `begin-step-0`, `proceed`, `confirm`, `compile-report`, `approve-decision`, `generate-excel`, `generate-pdf`

## Commands

| Command | What it does |
|---------|-------------|
| **[/kyc:onboard](./commands/onboard.md)** | Full customer onboarding with Step 0 independent verification, sanctions screening, PEP checks, risk scoring, and report generation |
| **[/kyc:onboard-interactive](./commands/onboard-interactive.md)** | Same workflow with step-by-step dialog guidance |
| **[/kyc:screen](./commands/screen.md)** | Standalone sanctions and PEP screening |
| **[/kyc:risk](./commands/risk.md)** | Risk reassessment with updated due diligence |
| **[/kyc:monitor](./commands/monitor.md)** | Transaction monitoring and AML reporting |
| **[/kyc:refresh](./commands/refresh.md)** | Periodic customer review |

## Getting Started

### Cowork

Upload this plugin folder to Cowork, then run:

```
/kyc:onboard-interactive "Jane Smith" -- UK resident, salaried employee, standard risk
```

### Claude Code

```bash
# Clone the repo
git clone https://github.com/vyayasan/kyc-analyst.git

# Install Python dependencies (for Excel and PDF generation)
pip install -r requirements.txt
```

See [QUICK_START_GUIDE.md](./QUICK_START_GUIDE.md) for a full walkthrough of your first case.

## What You Get

- **Step 0 Independent Verification** — 6 mandatory searches across 90+ sources before any due diligence begins
- **Deterministic Risk Scoring** — Four-factor weighted model with published formulas. Same inputs always produce the same score.
- **Excel Dashboard** — 4-sheet workbook (Executive Summary, Directorships, Discrepancies, Risk Assessment) via openpyxl
- **PDF Report** — 17-section compliance report via fpdf2
- **Case Folder** — Numbered folder structure (001-006) with immutable audit trail
- **Multi-jurisdiction** — UK/EU (AMLD5, MLR 2017, FCA), US (FinCEN, BSA/AML, OFAC), MENA (CBUAE, SAMA)

## Sample Output

See what the plugin actually produces — sanitized examples from a real onboarding run:

- **[Step 0 Verification Report](./docs/sample-output/SAMPLE-Step0-Report.md)** — Full 9-section report: customer profile, 6 search results, risk scoring calculation (showing the math), escalation check, decision, and compliance certification
- **[Audit Trail](./docs/sample-output/SAMPLE-Audit-Trail.txt)** — Immutable log of all 17 stagegates with timestamps, actors, consent keywords, and evidence references

The plugin also generates a **4-sheet Excel dashboard** (.xlsx) and a **6-page formatted PDF report** (.pdf) with identical content.

<details>
<summary>Case folder structure (click to expand)</summary>

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
├── 005_ESCALATION_BRIEF/           (only if escalation triggered)
└── 006_AUDIT_TRAIL/
    └── AUDIT_TRAIL.md              (immutable — locked after finalization)
```

</details>

## Data Sources

All free and public:

| Source | Coverage |
|--------|----------|
| OFAC SDN | US sanctions |
| UN Consolidated List | Global sanctions |
| EU Sanctions List | EU sanctions |
| UK HMT | UK sanctions |
| OpenSanctions PEP | 100+ countries |
| Companies House API | All UK entities |
| ICIJ Offshore Leaks | Panama Papers, Paradise Papers, Pandora Papers |
| SEC EDGAR | US public filings |

For premium sources (World-Check, LexisNexis, Dow Jones), add your own API keys via the connector system. See [CONNECTORS.md](./CONNECTORS.md).

## Workflow Templates

Five ready-to-use templates in [WORKFLOW_TEMPLATES.md](./WORKFLOW_TEMPLATES.md):

| Template | Use case | Estimated time |
|----------|----------|------|
| Template 1 | Salaried employee, standard risk | 15–20 min |
| Template 2 | HNWI, enhanced due diligence | 45–60 min |
| Template 3 | SME corporate onboarding | 30–40 min |
| Template 4 | Complex corporate, multi-jurisdiction | 60–90 min |
| Template 5 | Existing customer refresh | 20–30 min |

## Plugin Architecture

```
kyc-analyst/
├── .claude-plugin/plugin.json   # Plugin manifest
├── .mcp.json                    # Tool connections (connectors)
├── commands/                    # 6 slash commands mapped to regulatory workflows
│   ├── onboard.md               #   Full onboarding (1,047 lines, 17 stagegates)
│   ├── onboard-interactive.md   #   Interactive dialog mode
│   ├── screen.md                #   Sanctions + PEP screening
│   ├── risk.md                  #   Risk reassessment
│   ├── monitor.md               #   Transaction monitoring
│   └── refresh.md               #   Periodic review
├── skills/                      # Domain knowledge Claude draws on automatically
│   ├── onboarding/SKILL.md      #   Core onboarding logic + stagegates
│   ├── screening/SKILL.md       #   Sanctions + PEP screening logic
│   ├── risk-assessment/SKILL.md #   Deterministic risk scoring model
│   ├── monitoring/SKILL.md      #   Transaction monitoring patterns
│   └── refresh/SKILL.md         #   Periodic review triggers + logic
├── EXAMPLES/                    # 5 worked examples with expected outputs
│   ├── 1-Individual-Basic/
│   ├── 2-HNWI-EDD/
│   ├── 3-SME-Company/
│   ├── 4-Escalation-Case/
│   └── 5-Refresh-Case/
├── OUTPUT_TEMPLATES/            # Locked PDF, Excel, and case folder formats
├── docs/                        # Workflow diagram, demo slides, sample output
│   ├── kyc-analyst-workflow.svg #   17-stagegate workflow diagram (rendered in README)
│   ├── kyc-analyst-workflow.excalidraw  # Editable source (open at excalidraw.com)
├── WORKFLOW_TEMPLATES.md        # Copy-paste templates for 5 scenarios
├── QUICK_START_GUIDE.md         # 10-minute first case walkthrough
├── CONNECTORS.md                # Tool integration guide
├── MCP_INTEGRATION_GUIDE.md     # Detailed MCP tool usage patterns
└── requirements.txt             # Python dependencies (fpdf2, openpyxl)
```

### How the pieces connect

- **Skills** — Domain knowledge for onboarding, screening, risk assessment, transaction monitoring, and KYC refresh. Each skill defines mandatory stagegates that Claude follows automatically.
- **Commands** — Six slash commands you invoke explicitly. Each one maps to a regulatory workflow.
- **Connectors** — Tool-agnostic `~~placeholder` syntax that works with Google Drive, Box, Salesforce, Chrome, Slack, and others. Edit `.mcp.json` to point at your specific tool stack.
- **Stagegates** — 17 mandatory checkpoints requiring explicit analyst consent. No auto-approvals, no skipping, no proceeding on silence.

## Background

Built by [Vyayasan](https://github.com/vyayasan) — a product leader who has spent over a decade building fintech and compliance products at scale.

Previous work includes: co-founding an AI-powered financial crime compliance startup (selected for Google's inaugural AI First Accelerator — 1 of 16 UK startups from 500+ applicants, NVIDIA Inception member, pre-seed backed by institutional VCs with participation from executives at leading neobanks and cross-border payment companies), leading product at a global payment processor (100+ fintech clients, 47 countries, ML-based financial crime detection), and building the enterprise AI function at a UK specialist bank (Trust Layer architecture, human-in-the-loop workflows, FCA/PRA compliance).

Also an active open-source builder: AI code compliance scanner for EU AI Act, PCI DSS, and GDPR; API documentation transformer; contributor to AI Tinkerers community; speaker at Money20/20 Europe.

**The thesis:** foundation models have commoditized the integration layer that compliance platforms charge for. The data is free. The formulas are published. The workflows are well-understood. What remains valuable is domain expertise and human judgment — and those should be in the hands of analysts, not locked behind vendor subscriptions.

This is the first of several open-source compliance plugins. More at [Vyayasan](https://github.com/vyayasan).

## Roadmap

KYC Analyst is the first plugin on [OpenForge.ai](https://openforge.ai) — free, open-source AI plugins for compliance teams. All MIT licensed. All inspectable.

**Coming next:**

| Plugin | What it does | Status |
|--------|-------------|--------|
| **KYC Analyst** | KYC/AML onboarding, sanctions, PEP, risk scoring | ✅ Released |
| **Compliance Mailroom** | Gmail/Outlook monitoring, document triage, deadline tracking | 🔜 Coming soon |
| **Questionnaire Analyst** | Security questionnaires, vendor due diligence, client assessments | 🔜 Coming soon |
| **SAR Narrative Generator** | Suspicious Activity Report drafting (FinCEN BSA, FCA, VARA) | 🔜 Coming soon |
| **MLRO Report Generator** | Board-ready MLRO reports with trend analysis | 🔜 Coming soon |
| **Policy Drafter** | Draft compliance policies from regulatory text | 🔜 Coming soon |

**For this plugin:**

- [ ] Additional jurisdiction packs (APAC, LatAm)
- [ ] Corporate structure analysis with UBO identification
- [ ] Premium data source connectors (World-Check, LexisNexis, Dow Jones)
- [ ] Batch processing for portfolio-level screening

Have a feature request? [Open an issue](https://github.com/vyayasan/kyc-analyst/issues) or submit a PR.

## Disclaimer

**This plugin is an experimental open-source tool provided "as is" under the MIT License. It is not a substitute for professional legal, regulatory, or compliance advice.**

- **Not a regulated product.** This plugin is not a licensed compliance platform, not a regulated service, and not approved or endorsed by any regulatory authority (FCA, FinCEN, or otherwise).
- **Research preview platform.** Claude Cowork and Claude plugins are currently in research preview by Anthropic. Features, availability, and behavior may change without notice.
- **No guarantees of accuracy.** While this plugin queries public data sources, it cannot guarantee the accuracy, completeness, or timeliness of results. All outputs must be independently verified by a qualified compliance professional.
- **Human judgment required.** The 17 stagegates exist because AI cannot and should not make compliance decisions autonomously. Every decision in this workflow requires a trained analyst's review and approval.
- **Not legal advice.** Nothing in this plugin constitutes legal or regulatory advice. Consult qualified legal counsel for your jurisdiction.
- **Your responsibility.** Users are solely responsible for ensuring that their use of this plugin complies with applicable laws, regulations, and their firm's internal policies. The author accepts no liability for regulatory actions, fines, or losses arising from use of this tool.
- **Data source limitations.** Public data sources (OFAC, UN, Companies House, etc.) may have latency, gaps, or errors. Premium sources are not included. Screening results from this tool should supplement — not replace — your existing compliance infrastructure.
- **Pilot results are illustrative.** The early results reported above are from a single unaudited pilot and should not be treated as benchmarks or guarantees.

**If in doubt, consult your compliance officer and legal team before deploying this or any automated tool in a production compliance workflow.**

## FAQ

<details>
<summary><strong>Is this actually compliant with AMLD5 / MLR 2017?</strong></summary>

This plugin implements the workflow structure described in these regulations (independent verification per Article 10, risk-based approach, ongoing monitoring). However, the plugin itself is not a regulated product and has not been certified by any regulatory authority. Your firm's MLRO and legal team should evaluate whether it meets your specific compliance obligations. The 17 stagegates exist specifically to keep a trained human in control of every decision.
</details>

<details>
<summary><strong>Can this replace World-Check / ComplyAdvantage / LexisNexis?</strong></summary>

Not directly. Those platforms provide proprietary data (enhanced PEP lists, beneficial ownership databases, watchlists). This plugin uses only free public sources (OFAC, UN, EU, UK HMT, Companies House, OpenSanctions, ICIJ). For many small teams doing standard CDD on low-to-medium risk individuals, public sources may be sufficient. For enhanced due diligence, you will likely still need premium data — the connector system supports adding those APIs.
</details>

<details>
<summary><strong>How does it handle false positives in sanctions screening?</strong></summary>

The plugin presents all potential matches to the analyst at the relevant stagegate and waits for their assessment. It does not auto-dismiss or auto-confirm matches. Common name matches, partial matches, and date-of-birth mismatches are flagged for the analyst to evaluate. The analyst's decision is recorded in the immutable audit trail.
</details>

<details>
<summary><strong>What happens with non-English names or transliterated names?</strong></summary>

The plugin searches using the name as provided plus any declared aliases. For transliterated names, the analyst should add all known romanizations as aliases in the initial information-gathering stage. The OFAC SDN list includes alternate spellings, and OpenSanctions handles transliteration variants. However, this is a known limitation — comprehensive multilingual name matching requires specialized tooling.
</details>

<details>
<summary><strong>Is the risk model validated?</strong></summary>

The four-factor model uses published regulatory guidance (FATF, EBA, FinCEN) for its weight structure. It is deterministic — same inputs always produce the same score. It has not been independently validated or back-tested against a large dataset. Your firm should calibrate the weights and thresholds to match your risk appetite. The model is transparent (you can see the exact calculation in every report) and can be modified in `skills/risk-assessment/SKILL.md`.
</details>

<details>
<summary><strong>Why 17 stagegates? Isn't that slow?</strong></summary>

Regulatory compliance requires demonstrable human oversight. Each stagegate maps to a specific regulatory requirement (data verification, search authorization, evidence review, risk approval, escalation check, report generation). In practice, most gates take seconds to pass — the analyst reviews the presented evidence and types a keyword like `proceed` or `confirm`. The pilot showed 27 minutes end-to-end for a standard case, including all 17 gates.
</details>

<details>
<summary><strong>Can I use this in production?</strong></summary>

Claude Cowork and plugins are in research preview. This plugin is experimental. One fintech has used it in a supervised pilot. Whether it is suitable for your production compliance workflow depends on your firm's risk appetite, regulatory obligations, and legal assessment. See the full Disclaimer above.
</details>

## Security

Found a vulnerability? Report it privately to sandi@vyayasan.com. See [SECURITY.md](./SECURITY.md) for our responsible disclosure policy.

## Contributing

Plugins are just markdown files. Fork the repo, make your changes, and submit a PR. See [CONTRIBUTING.md](./CONTRIBUTING.md) for details on testing, stagegate rules, and jurisdiction support.

Looking for contributors who work in compliance (any country) to add jurisdiction-specific workflows.

## License

[MIT](./LICENSE)

---

<p align="center">
  <a href="https://star-history.com/#vyayasan/kyc-analyst&Date">
    <img src="https://api.star-history.com/svg?repos=vyayasan/kyc-analyst&type=Date" alt="Star History Chart" width="600"/>
  </a>
</p>

<p align="center">
  <a href="https://github.com/vyayasan/kyc-analyst/graphs/contributors">
    <img src="https://contrib.rocks/image?repo=vyayasan/kyc-analyst" alt="Contributors"/>
  </a>
</p>

<p align="center">
  <sub>Software free. Expertise paid. — <a href="https://openforge.ai">OpenForge.ai</a></sub>
</p>
