# Contributing to KYC Analyst

Thank you for your interest in contributing. This plugin is open source under the MIT license.

## Ways to Contribute

### 1. Use It and Report Issues
Run the plugin on real workflows. If something breaks or behaves unexpectedly, open a GitHub issue with:
- Which command you ran (e.g., `/kyc:onboard`)
- What you expected to happen
- What actually happened
- Your Claude Cowork version

### 2. Improve Documentation
- Fix typos, clarify instructions, add examples
- Translate documentation to other languages
- Add FAQ entries from your experience

### 3. Add Jurisdiction Support
- Add risk scoring models for new countries
- Add new sanctions list sources
- Add new company registry integrations
- Document regulatory requirements for your jurisdiction

### 4. Improve Workflows
- Suggest improvements to stagegate logic
- Add new workflow templates (e.g., KYB corporate onboarding for specific sectors)
- Improve Excel/PDF report formatting

### 5. Build Connectors
- Add templates for premium data sources (World-Check, LexisNexis, etc.)
- Add CRM integrations (Salesforce, HubSpot connector templates)
- Add cloud storage workflows

## Development Setup

### Prerequisites
- Claude Cowork (macOS or Windows)
- Claude Pro subscription
- Python 3.10+ (for report generation)
- Git

### Local Setup
```bash
git clone https://github.com/vyayasan/kyc-analyst.git
cd kyc-analyst
pip install -r requirements.txt
```

### Testing Your Changes
1. Copy modified files to your Cowork skills directory
2. Run one of the 5 example cases in `EXAMPLES/`
3. Verify all 17 stagegates fire correctly
4. Verify Excel + PDF output generates without errors
5. Check audit trail JSON is complete

### Example Test Run
```
# In Claude Cowork, run:
/kyc:onboard "Test Individual" -- UK resident, low risk, standard CDD

# Verify:
- All 17 stagegates prompt for consent
- Step 0 searches complete (6 mandatory)
- Risk score calculates correctly
- Excel generates 4 sheets
- PDF generates 17 sections
- Case folder creates numbered structure
```

## Pull Request Process

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/add-singapore-registry`)
3. Make your changes
4. Test with at least one example case end-to-end
5. Update documentation if you changed workflows
6. Submit a pull request with:
   - What you changed and why
   - Which example case(s) you tested with
   - Screenshots of output if relevant

## Code Style

- Markdown files: Use consistent heading levels, bullet formatting
- SKILL.md files: Follow the existing stagegate pattern (GATE → PRESENT → WAIT → PROCEED)
- Command files: Include usage examples and expected outputs
- Keep line lengths reasonable (< 120 chars where possible)

## Commit Messages

Format: `type: short description`

Types:
- `feat:` New feature (new command, new jurisdiction)
- `fix:` Bug fix
- `docs:` Documentation change
- `refactor:` Restructuring without behaviour change
- `test:` Adding or updating test cases

Examples:
```
feat: add Singapore MAS registry integration
fix: risk score rounding error for MEDIUM band
docs: add FAQ about premium data source setup
```

## Stagegate Rules (CRITICAL)

If you modify any workflow, these rules are **non-negotiable**:

1. **Never skip a stagegate.** Every HITL checkpoint must prompt and wait.
2. **Never auto-approve.** The plugin must wait for explicit human confirmation.
3. **Never proceed on silence.** If the analyst doesn't respond, the workflow pauses.
4. **Always log.** Every action must be recorded in the audit trail.
5. **Always present evidence.** Show the analyst what was found before asking for a decision.

These aren't preferences — they're regulatory requirements.

## Questions?

- Open a GitHub Discussion for general questions
- Open an Issue for bugs or feature requests
- Connect on LinkedIn: [Sandipanee Samantaray](https://linkedin.com/in/sandipanee)

## License

By contributing, you agree that your contributions will be licensed under the MIT License.
