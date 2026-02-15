# KYC Analyst v1.0.0 - Workflow Templates

**Version:** 1.0.0
**Author:** Vyayasan
**Purpose:** Ready-to-use workflow prompts for common KYC scenarios

---

## How to Use These Templates

1. **Choose a scenario** that matches your case type
2. **Copy the template** for that scenario
3. **Replace placeholders** in [brackets] with actual information
4. **Paste into Claude** and execute
5. **Review outputs** and make decisions

All templates include v1.0.0 features:
- 17 mandatory stagegates with explicit analyst consent
- Step 0 mandatory verification (5+1 independent searches including ICIJ)
- 90+ database sources
- Deterministic four-factor risk scoring
- 4-sheet Excel dashboard (openpyxl)
- 17-section PDF report (fpdf2)
- MCP connector integration (~~browser, ~~excel, ~~pdf)
- Immutable audit trail with HITL consent logging
- Case folder auto-creation (001-006 numbered structure)

**Stagegate Reference:** See `commands/onboard.md` for full 17-stagegate specification.
**Connector Reference:** See `CONNECTORS.md` for MCP tool integration.

---

## Template 1: Individual Client - Standard Employment

**Use for:** Salaried employees, standard risk profile

```
Execute KYC onboarding with Step 0 verification for individual client.

CLIENT DETAILS:
- Full Name: [e.g., John Smith]
- Date of Birth: [DD/MM/YYYY]
- Nationality: [Country]
- Country of Residence: [Country]
- Occupation: [Job Title]
- Employer: [Company Name]
- Expected Activity: Salary deposits, personal expenses

DOCUMENTS PROVIDED:
- [✓] Valid passport/ID
- [✓] Proof of address (utility bill/bank statement <3 months)
- [✓] Employment contract/payslips
- [✓] Application form with declarations

STEP 0 - MANDATORY VERIFICATION:

Search 1: Adverse Media
- Search 72+ adverse media sources (Google News, BBC, Reuters, Financial Times, legal databases)
- Check for: criminal records, fraud allegations, regulatory actions, sanctions
- Document: CLEAR or FINDINGS

Search 2: Directorships
- Use Companies House officer search or equivalent registry
- Identify ALL company directorships (disclosed and undisclosed)
- **CRITICAL:** This catches hidden business interests
- Document: List all companies with disclosure status

Search 3: PEP Status
- Check 5 PEP databases (EveryPolitician, Wikidata, UK Parliament, Register of Interests, CIA World Factbook)
- Screen for politically exposed person status
- Check family members if applicable
- Document: PEP or NOT PEP (with tier if applicable)

Search 4: Professional Background
- Verify employment via LinkedIn, company website, business news
- Confirm occupation claims match online presence
- Identify any discrepancies between declared and actual
- Document: VERIFIED or DISCREPANCIES

Search 5: Sanctions/Crime
- Screen against: OFAC SDN, EU Consolidated List, UK HM Treasury, UN Sanctions, Interpol
- Use 12 sanctions/legal sources
- Document: CLEAR or MATCH (assess false positive)

STEP 0 DECISION GATE:
- If all searches CLEAR → PROCEED to CDD
- If undisclosed directorships or material discrepancies → ESCALATE to Manager + MLRO

THEN GENERATE:
1. 4-sheet Excel Dashboard:
   - Sheet 1: Executive Summary (customer profile, all 5 search results, decision)
   - Sheet 2: Directorships (all companies with disclosure status)
   - Sheet 3: Discrepancies (declared vs actual comparison)
   - Sheet 4: Risk Assessment (Geographic 30%, Customer 35%, Product 25%, Channel 10%)

2. 17-section PDF Report:
   - Professional styling, client-ready format
   - Complete verification evidence
   - Heuristic risk score (automatic calculation)
   - Risk bands: LOW (0-20), MEDIUM (21-60), HIGH (61-100)

3. Case Folder: KYC-[YYYYMMDD]-ONB-[LASTNAME]-[SEQ]
   - 001_CASE_METADATA/
   - 002_STEP_0_SEARCHES/
   - 003_VERIFICATION_OUTCOMES/
   - 004_DECISION_DOCUMENTATION/
   - 005_ESCALATION_BRIEF/ (if needed)
   - 006_AUDIT_TRAIL/ (auto-generated, immutable)

FINAL DECISION:
- State: PROCEED or ESCALATE
- Risk Rating: LOW / MEDIUM / HIGH / CRITICAL
- Next Steps: Continue to CDD or escalate for EDD

Save all outputs to ~~cloud storage under KYC/Cases/2026/
```

**Expected Time:** 15-20 minutes
**Expected Result:** PROCEED with LOW-MEDIUM risk rating for standard employment

---

## Template 2: High Net Worth Individual (HNWI) - Enhanced Due Diligence

**Use for:** HNWI, large deposits, complex source of wealth

```
Execute Enhanced Due Diligence (EDD) onboarding with comprehensive verification.

CLIENT PROFILE:
- Full Name: [e.g., Alexander Thompson]
- Nationality: [Country]
- Estimated Net Worth: [£X million / $X million]
- Primary Source of Wealth: [e.g., Business ownership, Inheritance, Investment portfolio]
- Expected Activity: [e.g., Large wire transfers, investment transactions, international payments]
- Relationship Purpose: [e.g., Private banking, wealth management, investment account]

DOCUMENTS PROVIDED:
- [✓] Valid passport
- [✓] Proof of address (recent utility bill)
- [✓] Wealth source documentation (business accounts, inheritance papers, investment statements)
- [✓] Bank statements (6 months)
- [✓] Tax returns (2 years)

STEP 0 - ENHANCED VERIFICATION (All 5 searches MANDATORY):

Search 1: Adverse Media (COMPREHENSIVE)
- Use all 72+ sources across 11 tiers
- Include: ICIJ offshore leaks (Panama Papers, Paradise Papers, Pandora Papers, WikiLeaks)
- Search for: criminal allegations, fraud, corruption, regulatory enforcement, litigation
- Geographic focus: [Country of wealth origin]
- Time period: Last 10 years
- Document: CLEAR or FINDINGS with context

Search 2: Directorships (EXHAUSTIVE)
- Search all jurisdictions where client has operated
- Use: Companies House (UK), equivalent registries (US, EU, offshore)
- Map complete directorship history
- Identify active vs resigned positions
- Cross-reference with declared business interests
- **FLAG:** Any undisclosed companies = material misrepresentation
- Document: Complete directorship list with timeline

Search 3: PEP Status (EXTENDED)
- Check 5 explicit PEP databases
- **Important for HNWI:** Search family members, close associates, business partners
- Assess PEP tier if applicable (Tier 1 = highest risk)
- Consider: Former PEPs retain risk for 12+ months
- Document: PEP status with family/associate connections

Search 4: Professional Background (DETAILED)
- Verify business ownership claims (company accounts, registry records)
- Verify career history (LinkedIn, news archives, trade publications)
- Verify investment activities (if claimed)
- Assess reputational risk (industry standing, media coverage)
- **Cross-check:** Source of wealth narrative vs public evidence
- Document: VERIFIED or DISCREPANCIES

Search 5: Sanctions/Crime (COMPREHENSIVE)
- Use all 12 sanctions/legal sources
- Include: OpenSanctions, UK Court records, Companies House insolvencies
- Check for: sanctions, criminal convictions, CCJs, bankruptcy, insolvency
- Screen business entities owned/controlled
- Document: CLEAR or MATCH

ENHANCED RESEARCH:
- Source of Wealth Analysis:
  - How was wealth accumulated? (business sale, inheritance, investments, etc.)
  - Timeline of wealth accumulation
  - Evidence supporting narrative
  - Any red flags (rapid wealth, unclear origins, offshore structures)

- Source of Funds Analysis:
  - Origin of specific funds for this relationship
  - Bank statements showing fund flow
  - Tax documentation supporting legitimate income
  - Any third-party payments or complex routing

- Business Interests:
  - Complete ownership structure if business-derived wealth
  - Industry risk assessment
  - Geographic risk (high-risk jurisdictions?)
  - Beneficial ownership verification

STEP 0 DECISION GATE:
- **PROCEED if:** All verifications clear, wealth/funds explained, no material discrepancies
- **ESCALATE if:** PEP status, undisclosed interests, unexplained wealth, high-risk jurisdictions, adverse findings

HEURISTIC RISK SCORING:
System calculates automatic risk score based on:
- Geographic risk (client jurisdiction, wealth origin, transaction countries)
- Customer risk (PEP status, industry, source of wealth clarity)
- Product risk (account type, expected activity)
- Adverse findings (any red flags from searches)
- **HNWI inherent risk premium applied**

EDD REQUIREMENTS (if high risk):
- [ ] Senior management approval BEFORE onboarding
- [ ] Enhanced source of wealth documentation
- [ ] Enhanced source of funds documentation
- [ ] Detailed relationship purpose narrative
- [ ] Enhanced ongoing monitoring plan (6-month reviews)
- [ ] Transaction monitoring with lower thresholds

GENERATE OUTPUTS:
1. 4-sheet Excel Dashboard (EDD version):
   - Executive Summary with complete verification results
   - Directorships with ownership percentages
   - Source of Wealth analysis table
   - Enhanced Risk Assessment with justification

2. 17-section PDF Report (EDD standard):
   - Comprehensive background research
   - Detailed wealth/funds analysis
   - Complete screening results
   - Risk assessment with mitigations
   - Ongoing monitoring plan

3. Case Folder with 005_ESCALATION_BRIEF if needed

FINAL DECISION:
- Risk Rating: [Likely MEDIUM-HIGH for HNWI]
- EDD Level: Standard EDD / Enhanced EDD / Very High Risk
- Approval Required: [Compliance Manager / MLRO / Senior Management]
- Monitoring Plan: [6-month reviews, enhanced transaction monitoring]

Save to ~~cloud storage under KYC/Cases/2026/HNWI/
```

**Expected Time:** 45-60 minutes
**Expected Result:** MEDIUM-HIGH risk with EDD approval required

---

## Template 3: Small-Medium Enterprise (SME) - Corporate Onboarding

**Use for:** Standard SME companies, straightforward ownership

```
Execute corporate KYC onboarding with beneficial ownership verification.

COMPANY DETAILS:
- Legal Name: [e.g., Smith Manufacturing Limited]
- Trading Name: [if different]
- Registration Number: [Company number]
- Jurisdiction: [Country of incorporation]
- Date of Incorporation: [DD/MM/YYYY]
- Business Activity: [e.g., Manufacturing of industrial components]
- Expected Annual Turnover: [£X / $X]
- Expected Transaction Volume: [monthly/annual]

DOCUMENTS PROVIDED:
- [✓] Certificate of incorporation
- [✓] Articles of association / Memorandum
- [✓] Register of directors (current)
- [✓] Register of shareholders/members (current)
- [✓] Proof of registered office address
- [✓] Latest financial accounts
- [✓] Business website / trading evidence

BENEFICIAL OWNERSHIP (UBO) IDENTIFICATION:
Per AMLD5/UK MLR 2017 - identify all individuals with >25% ownership/control:

Expected UBO structure:
- [Name 1]: [X]% shareholding
- [Name 2]: [Y]% shareholding
- [If no qualifying UBO]: Senior Managing Official

**CRITICAL:** Verify complete ownership chain to natural persons

STEP 0 - ENTITY VERIFICATION:

Search 1: Adverse Media (ENTITY + DIRECTORS)
- Search company name in 72+ adverse media sources
- Search each director by name
- Check for: regulatory actions, litigation, fraud, insolvency
- Document: CLEAR or FINDINGS

Search 2: Directorships (ALL DIRECTORS + UBOs)
- Companies House search for each director
- Map all other directorships held
- Identify any high-risk company associations
- Check for phoenix companies (previous insolvencies)
- Document: Complete directorship map

Search 3: PEP Status (ALL UBOs + DIRECTORS)
- Screen each individual against 5 PEP databases
- Even minority shareholders if >25% threshold
- Document: PEP or NOT PEP for each person

Search 4: Business Background (ENTITY VERIFICATION)
- Verify business activity (website, Companies House description, accounts)
- Confirm company is trading (recent accounts filed, website active)
- Check industry reputation
- Assess business model credibility
- Document: VERIFIED or DISCREPANCIES

Search 5: Sanctions/Crime (ENTITY + ALL INDIVIDUALS)
- Screen company against 12 sanctions lists
- Screen all directors and UBOs
- Check for: sanctions, CCJs, insolvencies, criminal records
- Document: CLEAR or MATCH

OWNERSHIP STRUCTURE VERIFICATION:
- Build complete ownership tree showing:
  - All shareholders with percentages
  - Ultimate beneficial owners (>25%)
  - Any parent companies or group structure
  - Any trusts or nominee arrangements

- Assess transparency:
  - Clear ownership? (GREEN)
  - Some nominee shareholding? (AMBER - requires explanation)
  - Complex offshore structure? (RED - requires enhanced scrutiny)

INDUSTRY & GEOGRAPHIC RISK ASSESSMENT:
- Industry Risk: [HIGH / MEDIUM / LOW]
  - High: MSB, gambling, precious metals, real estate, crypto
  - Medium: Professional services, import/export, construction
  - Low: Retail, manufacturing, technology, healthcare

- Geographic Risk: [HIGH / MEDIUM / LOW]
  - Consider: Jurisdiction of incorporation, trading locations, customer base
  - High-risk jurisdictions requiring enhanced scrutiny

STEP 0 DECISION GATE:
- **PROCEED if:** Ownership clear, all screenings clear, business verified
- **ESCALATE if:** Complex ownership, PEPs identified, adverse findings, high-risk industry/geography

GENERATE OUTPUTS:
1. 4-sheet Excel Dashboard:
   - Sheet 1: Company Profile + Verification Summary
   - Sheet 2: Ownership Structure (visual tree diagram)
   - Sheet 3: Director/UBO Screening Results (table format)
   - Sheet 4: Corporate Risk Assessment (industry, geography, ownership factors)

2. 17-section PDF Report:
   - Corporate profile
   - Complete ownership structure
   - All individual screening results
   - Business verification evidence
   - Risk assessment and rating

3. Case Folder: KYC-[YYYYMMDD]-ONB-[COMPANYNAME]-[SEQ]

CDD REQUIREMENTS (if proceeding):
- [ ] Verify all UBO identities (passport/ID)
- [ ] Verify all UBO addresses
- [ ] Confirm source of funds for expected transactions
- [ ] Understand business relationship purpose
- [ ] Set appropriate transaction monitoring limits

FINAL DECISION:
- Ownership Transparency: [CLEAR / COMPLEX / OPAQUE]
- Risk Rating: [LOW / MEDIUM / HIGH]
- Approval Level: [Analyst / Senior Analyst / Manager]
- Monitoring Plan: [Annual review / Bi-annual / Quarterly]

Save to ~~cloud storage under KYC/Cases/2026/Corporate/SME/
```

**Expected Time:** 30-40 minutes
**Expected Result:** MEDIUM risk, ownership clear, PROCEED with CDD

---

## Template 4: Complex Corporate Structure - Multi-Jurisdiction

**Use for:** Multi-layer ownership, offshore entities, complex groups

```
Execute Enhanced Corporate Due Diligence for complex structure.

GROUP STRUCTURE:
- Operating Entity: [Company A, Registration: XX123456, Jurisdiction: UK]
- Immediate Parent: [Company B, Registration: YY789012, Jurisdiction: Jersey]
- Ultimate Parent: [Company C, Registration: ZZ345678, Jurisdiction: Cayman Islands]
- Number of Layers: [e.g., 3 layers]
- Jurisdictions Involved: [UK, Jersey, Cayman Islands]

COMPLEXITY INDICATORS:
- [✓] Multiple jurisdictions (2+)
- [✓] Offshore entities present
- [✓] Nominee shareholders/directors
- [ ] Trust structures
- [ ] Bearer shares
- [ ] Multiple currency flows expected

DOCUMENTS PROVIDED:
- [✓] Certificate of incorporation (all entities)
- [✓] Group structure chart
- [✓] Shareholder registers (all levels)
- [✓] Director registers (all levels)
- [✓] Financial accounts (operating entity)
- [✓] UBO declaration
- [✓] Explanation for structure complexity

**CRITICAL QUESTIONS TO ANSWER:**
1. Who ultimately owns/controls this structure? (Natural persons)
2. What is the commercial rationale for complexity?
3. Are there legitimate tax/business reasons for offshore entities?
4. Is the structure transparent or opaque?

STEP 0 - ENHANCED ENTITY VERIFICATION (ALL LAYERS):

For EACH entity in the chain:

Search 1: Adverse Media
- Search entity name in 72+ sources
- Include ICIJ offshore leaks (Panama Papers, Paradise Papers, Pandora Papers)
- **Critical:** Offshore entities often appear in leaked databases
- Search jurisdiction-specific regulatory actions
- Document: CLEAR or FINDINGS for each entity

Search 2: Directorships (COMPLETE CHAIN)
- Map all directors at every layer
- Identify professional nominee directors (corporate services firms)
- **Red flag:** Same nominees appearing across unrelated structures
- Trace director network across jurisdictions
- Document: Complete director map with nominee identification

Search 3: PEP Status (ALL INDIVIDUALS IN CHAIN)
- Screen every natural person: UBOs, directors, shareholders
- Include intermediate holding company directors
- **Important:** PEPs often use offshore structures
- Document: PEP status for each individual

Search 4: Business Background (GROUP-LEVEL)
- Verify operating entity's actual business activity
- Assess whether structure matches business needs
- **Question:** Why is a [simple business] owned through [complex offshore structure]?
- Research group's public reputation
- Check for previous regulatory issues
- Document: Business rationale JUSTIFIED or QUESTIONABLE

Search 5: Sanctions/Crime (COMPREHENSIVE - ALL ENTITIES & INDIVIDUALS)
- Screen every entity in the chain
- Screen every director, shareholder, UBO
- Check for: sanctions, financial crime, regulatory actions
- **Offshore entities:** Higher risk of sanction evasion
- Document: CLEAR or MATCH

BENEFICIAL OWNERSHIP PENETRATION:
**Must trace through all layers to natural persons:**

Layer 1 (Operating Entity):
- Shareholder: [Company B] 100%

Layer 2 (Intermediate Holding):
- Shareholder: [Company C] 100%
- Directors: [Names - identify if nominees]

Layer 3 (Ultimate Holding):
- Shareholders: [Mr. X] 60%, [Mr. Y] 40%
- Directors: [Names - identify if nominees]

**Ultimate Beneficial Owners:**
- Mr. X: 60% indirect ownership → VERIFY IDENTITY
- Mr. Y: 40% indirect ownership → VERIFY IDENTITY

**Complexity Analysis:**
- Number of intermediary layers: [X]
- Offshore jurisdictions involved: [List]
- Commercial rationale: [e.g., "Tax efficiency for international trading" vs "No clear rationale"]
- Transparency assessment: [TRANSPARENT / MODERATE / OPAQUE]

JURISDICTION RISK ASSESSMENT:
For each jurisdiction, assess:
- Tax haven status (Cayman, BVI, etc.)
- Financial secrecy index rating
- AML/CFT compliance (FATF ratings)
- Beneficial ownership disclosure requirements
- Corporate services industry prevalence

**Red flags:**
- [ ] Multiple offshore layers without clear business need
- [ ] Jurisdictions with weak AML/CFT frameworks
- [ ] Professional nominee shareholders concealing true ownership
- [ ] Bearer shares or trust structures obscuring ownership
- [ ] Rapid changes to structure before onboarding

STEP 0 DECISION GATE:
- **ESCALATE** (almost certainly for complex offshore structures)
- Requires senior management review
- Enhanced due diligence mandatory
- Need clear commercial rationale for structure complexity
- **Reject** if unable to identify UBOs or rationale not credible

ENHANCED DUE DILIGENCE REQUIREMENTS:
- [ ] Senior management approval (MLRO + CFO/CEO)
- [ ] Detailed explanation for structure (written business case)
- [ ] Independent verification of UBO identities (certified documents)
- [ ] Enhanced source of funds documentation (showing clean origin)
- [ ] Purpose of relationship (why using our services)
- [ ] Expected transaction patterns (must be consistent with business)
- [ ] Enhanced monitoring plan (quarterly reviews minimum)
- [ ] Ongoing reporting of structure changes

GENERATE OUTPUTS:
1. 4-sheet Excel Dashboard:
   - Sheet 1: Executive Summary with structure complexity assessment
   - Sheet 2: Multi-Layer Ownership Diagram (visual with all entities)
   - Sheet 3: Complete Screening Results (all entities and individuals)
   - Sheet 4: Enhanced Risk Assessment (layer-by-layer risk scoring)

2. 17-section PDF Report:
   - Complete group structure analysis
   - Jurisdiction risk assessment
   - Commercial rationale evaluation
   - All screening evidence
   - Enhanced risk assessment
   - Recommended monitoring plan

3. Case Folder: KYC-[YYYYMMDD]-ONB-[GROUPNAME]-[SEQ]
   - MUST include 005_ESCALATION_BRIEF/

FINAL DECISION (Escalation Required):
- Structure Complexity: [HIGH / VERY HIGH]
- Transparency: [TRANSPARENT / MODERATE / OPAQUE]
- Commercial Rationale: [JUSTIFIED / UNCLEAR / NOT CREDIBLE]
- Risk Rating: [HIGH / VERY HIGH / CRITICAL]
- Recommendation: [APPROVE WITH EDD / ADDITIONAL INFO NEEDED / REJECT]
- Monitoring Plan: [Quarterly enhanced reviews, structure change notification]

Escalate to: Manager + MLRO + Senior Management
Send: Complete evidence package + structure diagram + risk assessment

Save to ~~cloud storage under KYC/Cases/2026/Corporate/Complex/
```

**Expected Time:** 60-90 minutes
**Expected Result:** HIGH risk, escalation to senior management, EDD required

---

## Template 5: KYC Refresh - Periodic Review (Individual)

**Use for:** Existing customers, periodic review requirement

```
Execute KYC refresh for existing individual customer.

CUSTOMER REFERENCE:
- Customer ID: [Internal reference]
- Original Onboarding Date: [DD/MM/YYYY]
- Last Review Date: [DD/MM/YYYY]
- Current Risk Rating: [LOW / MEDIUM / HIGH]
- Review Frequency: [Annual / Bi-annual / Quarterly]
- Relationship Type: [e.g., Personal banking, investment account]

REFRESH TRIGGER:
- [ ] Scheduled periodic review (due date reached)
- [ ] Risk rating change (escalated to higher tier)
- [ ] Material change in circumstances (new wealth, new business)
- [ ] Regulatory requirement
- [ ] Transaction monitoring alert

CURRENT CUSTOMER INFORMATION:
- Full Name: [Name]
- Date of Birth: [DD/MM/YYYY]
- Current Address: [Address]
- Current Occupation: [Job title / Business]
- Source of Wealth: [Previously verified source]

REFRESH OBJECTIVES:
1. Confirm no material changes to circumstances
2. Re-verify current information
3. Update screening (sanctions, PEPs, adverse media)
4. Assess ongoing risk rating
5. Confirm relationship purpose still valid

STEP 0 - REFRESH VERIFICATION:

Search 1: Adverse Media (SINCE LAST REVIEW)
- Focus on period since last review: [Date] to present
- Use 72+ sources
- Look for new: criminal charges, fraud allegations, regulatory actions, litigation
- **Compare:** Any new findings vs clean previous review?
- Document: NO CHANGE or NEW FINDINGS

Search 2: Directorships (UPDATE)
- Re-check Companies House for any new directorships
- **Critical:** Identify new undisclosed business interests since last review
- Compare with previous directorship list
- Document: NO CHANGE or NEW DIRECTORSHIPS (with disclosure assessment)

Search 3: PEP Status (RE-SCREEN)
- Re-check 5 PEP databases
- **Consider:** Customer may have entered/exited PEP status since last review
- Former PEPs: Assess if risk period expired
- New PEPs: Immediate escalation required
- Document: NO CHANGE or STATUS CHANGE

Search 4: Professional Background (UPDATE)
- Verify current employment status (LinkedIn, company website)
- **Compare:** Still at same employer? Same industry?
- Any career changes that affect risk (e.g., moved to high-risk industry)?
- Document: NO CHANGE or MATERIAL CHANGES

Search 5: Sanctions/Crime (RE-SCREEN)
- Re-screen against 12 current sanctions/legal lists
- **Lists update regularly** - customer could be newly sanctioned
- Document: CLEAR or NEW MATCH

MATERIAL CHANGES ASSESSMENT:
Review for changes since last KYC:

Address Changes:
- Previous: [Old address]
- Current: [New address]
- Assessment: [Same country? Geographic risk change?]

Employment Changes:
- Previous: [Old employer/business]
- Current: [New employer/business]
- Assessment: [Industry risk change? Income level change?]

Source of Wealth Changes:
- Previous: [Previous source]
- Current: [Current source]
- **Critical:** New wealth requires source verification
- Assessment: [Consistent? New source needs documentation?]

Transaction Pattern Changes:
- Previous pattern: [Description]
- Current pattern: [Description]
- Assessment: [Consistent with profile? Unexplained changes?]

**Escalation Triggers:**
- [ ] New PEP status identified
- [ ] New adverse media findings
- [ ] Undisclosed new directorships
- [ ] Material change in wealth without explanation
- [ ] Transaction patterns inconsistent with profile
- [ ] Customer became sanctioned

REFRESH DECISION:
- **NO CHANGES:** Update screening, confirm risk rating, set next review
- **MINOR CHANGES:** Document changes, update records, continue monitoring
- **MATERIAL CHANGES:** Escalate for enhanced review, may require new verification
- **ADVERSE FINDINGS:** Immediate escalation, may require relationship exit

GENERATE OUTPUTS:
1. Refresh Summary Report (2-page):
   - Previous KYC summary
   - Current verification results
   - Changes identified
   - Updated risk assessment
   - Next review date

2. Updated Excel Dashboard (if material changes)

3. Update case folder: KYC-[ORIGINAL-REF]-REF-[YYYYMMDD]

UPDATE RISK RATING:
- Previous Risk: [LOW / MEDIUM / HIGH]
- Current Risk: [LOW / MEDIUM / HIGH]
- Change Rationale: [If changed, explain why]
- Next Review: [Date based on risk rating]

MONITORING PLAN:
- Low Risk: Review in [3-5 years]
- Medium Risk: Review in [1-2 years]
- High Risk/EDD: Review in [6-12 months]

Save to ~~cloud storage under KYC/Cases/2026/Refresh/
Update customer record in ~~CRM with refresh completion
```

**Expected Time:** 20-30 minutes
**Expected Result:** Most refreshes show NO CHANGE, confirm existing risk rating

---

## Quick Reference: When to Use Which Template

| Customer Type | Risk Level | Template | Time | Output |
|---------------|------------|----------|------|--------|
| Salaried employee | Low-Medium | Template 1 | 15-20 min | PROCEED |
| HNWI, entrepreneur | High | Template 2 | 45-60 min | EDD |
| SME, clear ownership | Medium | Template 3 | 30-40 min | CDD |
| Complex group, offshore | Very High | Template 4 | 60-90 min | Escalation |
| Existing customer | Varies | Template 5 | 20-30 min | Update |

---

## Connector Integration Examples

All templates work with MCP connectors:

**Cloud Storage:**
```
Save outputs to ~~cloud storage under KYC/Cases/2026/
```
Works with: Google Drive, Box, OneDrive, SharePoint, Dropbox

**CRM:**
```
Retrieve customer profile from ~~CRM for [Customer Name]
Update ~~CRM with completed KYC status
```
Works with: Salesforce, HubSpot, Dynamics

**Browser:**
```
Use ~~browser to search Companies House for [Company Name]
Use ~~browser to verify LinkedIn profile for [Person Name]
```
Works with: Claude in Chrome

---

## Notes

- All templates include **mandatory Step 0 verification** per v1.0.0 requirements
- **Heuristic risk scoring** is automatic based on search findings
- **Decision gate** (PROCEED/ESCALATE) is built into each workflow
- Outputs follow **locked template formats** for regulatory compliance
- **Audit trail** is auto-generated and immutable

For connector setup, see CONNECTORS.md
For quick start, see QUICK_START_GUIDE.md

---

**Version:** 1.0.0
**Author:** Vyayasan
**GitHub:** https://github.com/vyayasan/kyc-analyst
