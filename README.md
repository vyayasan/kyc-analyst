# KYC Analyst

Automates the research-intensive parts of KYC/AML compliance -- sanctions screening, adverse media searches, PEP checks, risk scoring, and report generation -- while keeping humans in control of every decision. Built for [Claude Cowork](https://claude.ai/cowork), also compatible with [Claude Code](https://claude.ai/code).

## Why This Plugin

Compliance analysts spend most of their time navigating public websites, screening free databases, and writing reports. The underlying data sources (OFAC, UN, EU sanctions lists, Companies House, OpenSanctions) are all free. The risk formulas (MLR 2017, FinCEN CDD) are published. This plugin orchestrates all of that while enforcing 17 mandatory human-in-the-loop checkpoints -- AI assists, the analyst decides.

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
/kyc:onboard "Jane Smith" -- UK resident, salaried employee, standard risk
```

### Claude Code

```bash
# Clone the repo
git clone https://github.com/vyayasan/kyc-analyst.git

# Install Python dependencies (for Excel and PDF generation)
pip install -r requirements.txt
```

See [QUICK_START_GUIDE.md](./QUICK_START_GUIDE.md) for a full walkthrough of your first case.

## How It Works

- **Skills** -- Domain knowledge for onboarding, screening, risk assessment, transaction monitoring, and KYC refresh. Each skill defines mandatory stagegates that Claude follows automatically.
- **Commands** -- Six slash commands you invoke explicitly. Each one maps to a regulatory workflow.
- **Connectors** -- Tool-agnostic `~~placeholder` syntax that works with Google Drive, Box, Salesforce, Chrome, Slack, and others. Edit `.mcp.json` to point at your specific tool stack.
- **Stagegates** -- 17 mandatory checkpoints requiring explicit analyst consent. No auto-approvals, no skipping, no proceeding on silence.

## What You Get

- **Step 0 Independent Verification** -- 6 mandatory searches across 90+ sources (adverse media, ICIJ Offshore Leaks, directorships, PEP status, professional background, sanctions) before any due diligence begins
- **Deterministic Risk Scoring** -- Four-factor weighted model (Geographic 30%, Customer 35%, Product 25%, Channel 10%) with published formulas. Same inputs always produce the same score.
- **Excel Dashboard** -- 4-sheet workbook (Executive Summary, Directorships, Discrepancies, Risk Assessment) generated via openpyxl
- **PDF Report** -- 17-section compliance report generated via fpdf2
- **Case Folder** -- Numbered folder structure (001-006) with immutable audit trail
- **Multi-jurisdiction** -- UK/EU (AMLD5, MLR 2017, FCA), US (FinCEN, BSA/AML, OFAC), MENA (CBUAE, SAMA)

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

For premium sources (World-Check, LexisNexis, Dow Jones), add your own API keys via the connector system.

## Workflow Templates

Five ready-to-use templates in [WORKFLOW_TEMPLATES.md](./WORKFLOW_TEMPLATES.md):

| Template | Use case | Time |
|----------|----------|------|
| Template 1 | Salaried employee, standard risk | 15-20 min |
| Template 2 | HNWI, enhanced due diligence | 45-60 min |
| Template 3 | SME corporate onboarding | 30-40 min |
| Template 4 | Complex corporate, multi-jurisdiction | 60-90 min |
| Template 5 | Existing customer refresh | 20-30 min |

## Plugin Structure

```
kyc-analyst/
├── .claude-plugin/plugin.json   # Manifest
├── .mcp.json                    # Tool connections
├── commands/                    # Slash commands you invoke explicitly
├── skills/                      # Domain knowledge Claude draws on automatically
├── EXAMPLES/                    # Five worked examples with expected outputs
├── OUTPUT_TEMPLATES/            # Locked PDF and case folder formats
├── WORKFLOW_TEMPLATES.md        # Copy-paste workflow templates
├── QUICK_START_GUIDE.md         # 10-minute first case walkthrough
├── CONNECTORS.md                # Tool integration guide
└── requirements.txt             # Python dependencies (fpdf2, openpyxl)
```

## Contributing

Plugins are just markdown files. Fork the repo, make your changes, and submit a PR. See [CONTRIBUTING.md](./CONTRIBUTING.md) for details on testing, stagegate rules, and jurisdiction support.

## License

MIT
