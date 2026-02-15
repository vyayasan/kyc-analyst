---
name: onboarding
description: >
  Full KYC customer onboarding with mandatory Step 0 independent verification (5+1 searches),
  17 sequential stagegates requiring explicit analyst consent, deterministic four-factor risk scoring,
  case folder auto-creation, 4-sheet Excel dashboard, 17-section PDF report, and immutable audit trail.
  Covers UK/EU (AMLD5), US (FinCEN CDD), and MENA jurisdictions.
user-invocable: true
category: compliance
estimated-duration: 30 minutes
---

# ONBOARDING SKILL.md - Complete Implementation
**Author:** Vyayasan
**Version:** 1.0.0
**Status:** Production Ready - Final Locked Version

---

## SKILL OVERVIEW

This SKILL defines the complete KYC onboarding workflow with mandatory Step 0 independent verification, case folder auto-creation, and locked template enforcement.

**Trigger:** `/kyc-analyst:onboard [Customer Name] [Country]`

**Stagegate Enforcement:** This skill enforces 17 mandatory stagegates with explicit analyst consent at each gate. See `commands/onboard.md` for the full stagegate specification.

**MCP Integration:** Uses ~~browser (Claude in Chrome) for web research, ~~excel (openpyxl) for dashboards, ~~pdf (fpdf2) for reports. See `CONNECTORS.md` for full connector reference.

---

## STEP 0: MANDATORY INDEPENDENT VERIFICATION

### Why Step 0 is Mandatory

**Regulatory Requirement:** AMLD5 Article 10(a) and UK MLR 2017 Regulation 19 require independent verification using "reliable, independent source documents, data or information."

**Analyst Compliance Duty:** Analyst must verify customer declarations independently. Cannot rely solely on what customer claims - must verify through independent sources.

**This Skill Enforces:** No proceeding to traditional onboarding until Step 0 is complete and clear.

### Step 0 Process Flow

```
COMMAND INVOKED
    ↓
CREATE CASE FOLDER (KYC-[DATE]-[TYPE]-[NAME]-[SEQ])
    ↓
BEGIN STEP 0 - INDEPENDENT VERIFICATION
    ↓
SEARCH 1: Adverse Media ─→ DOCUMENT FINDINGS
SEARCH 2: Directorships ─→ DOCUMENT FINDINGS
SEARCH 3: PEP Status ────→ DOCUMENT FINDINGS
SEARCH 4: Professional Background → DOCUMENT FINDINGS
SEARCH 5: Sanctions/Crime ──→ DOCUMENT FINDINGS
    ↓
ANALYSIS & DECISION
    ↓
All Clear? → YES → Proceed to Step 1
    ↓ NO (DISCREPANCIES FOUND)
ESCALATE → Manager Review Required
```

### Five Mandatory Searches - Detailed

#### SEARCH 1: ADVERSE MEDIA & NEWS
**Objective:** Identify any negative news, criminal records, regulatory violations, financial crime

**Search Strategy:**
```
Sources:
- Google News: "[Customer Name]" crime/fraud/scandal
- BBC News: "[Customer Name]" conviction
- Reuters: "[Customer Name]" regulatory action
- Companies House: Search for insolvency notices
- FCA Register: Check for regulatory action
- UK Media Index: General news scan
```

**What to Document:**
- Criminal records (yes/no)
- Regulatory violations (yes/no)
- Financial crime (yes/no)
- Bankruptcy/insolvency (yes/no)
- Adverse media (yes/no)

**Decision Rule:**
- All CLEAR → Continue to next search
- Any FINDINGS → Document, assess severity

#### SEARCH 2: COMPANY DIRECTORSHIPS
**Objective:** Identify ALL company involvement, directorships, beneficial ownership

**Search Strategy:**
```
Sources:
- Companies House: Direct officer search for [Customer Name]
- Companies House: Company search for any businesses
- Business registries: Director and shareholder registrations
- Corporate databases: Cross-verification
```

**What to Document:**
- Company name
- Position (director, shareholder, officer)
- Status (active/dormant)
- Appointment date
- Any conflicts or patterns
- Shell company assessment

**Critical Findings - Escalate If:**
- Multiple undisclosed directorships
- Director at company customer also works for
- Shell company patterns
- Beneficial ownership unclear

#### SEARCH 3: PEP STATUS (Politically Exposed Person)
**Objective:** Identify political exposure requiring Enhanced Due Diligence

**Search Strategy:**
```
Sources:
- UK Government PEP Database
- Electoral Commission (candidacy/office)
- International PEP Lists
- Government employee records
```

**What to Document:**
- Current political positions (yes/no)
- Previous political positions (yes/no)
- Family member PEP status (yes/no)
- Close associates with political exposure (yes/no)

**Decision Rule:**
- PEP identified → Triggers EDD
- Family PEP identified → Document relationship
- Clear → Continue

#### SEARCH 4: PROFESSIONAL BACKGROUND
**Objective:** Verify occupation claims independently

**Search Strategy:**
```
Sources:
- LinkedIn: Employment history, current roles
- Company websites: Staff directory, team pages
- Business registry: Company ownership, director roles
- News: Business announcements, funding rounds
```

**What to Document:**
- Current employment (company, position, title)
- Employment status (employed/self-employed/director)
- Business activities claimed vs. verified
- Professional credentials
- Income sources identified

**Critical Discrepancies - Escalate If:**
- Declared self-employed but employed elsewhere
- Undisclosed business roles or directorships
- Business claims cannot be verified
- Source of funds misrepresented
- Pattern of non-disclosure evident

#### SEARCH 5: SANCTIONS & FINANCIAL CRIME
**Objective:** Confirm no sanctions matches or financial crime involvement

**Search Strategy:**
```
Sources:
- OFAC Specially Designated Nationals List
- EU Consolidated Sanctions List
- UK Sanctions Regime
- UN Security Council Consolidated List
- Interpol Database
```

**What to Document:**
- OFAC match (yes/no)
- EU sanctions (yes/no)
- UK sanctions (yes/no)
- UN sanctions (yes/no)
- Criminal convictions (yes/no)
- Interpol notices (yes/no)

**Decision Rule:**
- Any match → IMMEDIATE ESCALATION
- All clear → Continue

### Step 0 Report Template

**File Created:** `STEP_0_VERIFICATION_REPORT.md` (LOCKED TEMPLATE)

**Required Sections:**
```markdown
# STEP 0 VERIFICATION REPORT

## Search 1: Adverse Media
[Findings documented]

## Search 2: Directorships
[All companies listed with details]

## Search 3: PEP Status
[PEP assessment]

## Search 4: Professional Background
[Occupation and business verification]

## Search 5: Sanctions & Crime
[Sanctions screening results]

## DECISION GATE ANALYSIS
[Summary of findings]

## Material Misrepresentation Assessment
[If discrepancies found]

## Step 0 Decision: [PROCEED / ESCALATE]
[Decision logic]

## Certification
[Analyst sign-off]
```

### Step 0 Decision Gate

**PROCEED Criteria (All Required):**
- ✓ All five searches completed
- ✓ No material discrepancies found
- ✓ Declarations verified or clarified
- ✓ No escalation triggers
- ✓ Step 0 Report signed off

**ESCALATE Criteria (Any Found):**
- ✗ Material misrepresentation identified
- ✗ Multiple undisclosed directorships
- ✗ Sanctions match found
- ✗ Financial crime indication
- ✗ PEP status requiring EDD
- ✗ Source of funds misrepresented
- ✗ Pattern of intentional non-disclosure

### Step 0 Escalation Routing

**Material Findings Escalate To:**
1. **Primary:** Compliance Manager (case assessment)
2. **Secondary:** MLRO (if money laundering concern)

**Information to Include:**
- Customer name and ID
- Critical findings summary
- Regulatory basis for escalation
- Recommended actions
- Supporting evidence

**Manager Decision Options:**
1. Proceed with EDD (Enhanced Due Diligence)
2. Contact customer for clarification
3. Decline relationship
4. Refer for SAR consideration

---

## STEP 1: TRADITIONAL ONBOARDING (Post-Step 0)

**Proceeds Only If:** Step 0 is complete and clear (or escalation resolved)

### Collection Phase

Gather required information:
- Full personal identification (passport, ID)
- Current address verification
- Employment/business details
- Source of funds documentation
- Beneficial ownership (if applicable)
- PEP disclosure
- Sanctions screening confirmation

### Documentation Phase

Create case documents:
- Customer profile
- Risk assessment
- Due diligence summary
- Evidence file

### Approval Phase

- Compliance manager review
- MLRO sign-off (if required)
- Final approval decision

---

## CASE FOLDER AUTO-CREATION

### Naming Convention
`KYC-[YYYYMMDD]-[TYPE_CODE]-[CUSTOMER_NAME]-[SEQUENCE]`

**Components:**
- **YYYYMMDD:** Application date
- **TYPE_CODE:** ONB (onboarding), SCR (screening), REF (refresh), RAS (risk), AML (monitoring)
- **CUSTOMER_NAME:** Last name (max 20 chars)
- **SEQUENCE:** 001, 002, 003, etc. (handles multiple applications same date)

**Example:** `KYC-20260202-ONB-SMITH-001`

### Automatic Folder Structure

Plugin creates (automatically):
```
001_CASE_METADATA/
├── CASE_METADATA.md (LOCKED TEMPLATE)

002_STEP_0_VERIFICATION/
├── STEP_0_VERIFICATION_REPORT.md (LOCKED TEMPLATE)
├── 001_Adverse_Media/
│   └── Search_1_Findings.md
├── 002_Directorships/
│   └── Search_2_Findings.md
├── 003_PEP_Status/
│   └── Search_3_Findings.md
├── 004_Professional_Background/
│   └── Search_4_Findings.md
└── 005_Sanctions_Crime/
    └── Search_5_Findings.md

003_EVIDENCE/
├── Identification documents
├── Address verification
├── Employment confirmation
└── Source of funds documentation

004_AUDIT_TRAIL/
├── AUDIT_TRAIL.md (LOCKED TEMPLATE)

005_ESCALATIONS/
├── ESCALATION_BRIEF.md (if applicable)
└── Manager Decision.md (if applicable)

006_COMMUNICATIONS/
├── Customer correspondence
└── Customer clarification requests

KYC_[CustomerName]_Findings_Report.xlsx
├── Executive Summary sheet
├── Step 0 Results sheet
├── Discrepancies sheet
└── Risk Assessment sheet
```

---

## LOCKED TEMPLATES - IMMUTABLE FORMAT

### Template 1: CASE_METADATA.md
**Purpose:** Single source of truth for case identification

**Structure (Locked):**
```markdown
# CASE METADATA - LOCKED TEMPLATE

## CASE IDENTIFICATION
Case ID, Type, Customer, Application Date, Analyst

## CUSTOMER DETAILS
Name, Email, Nationality, Residence, DOB, Passport

## DECLARED BUSINESS PROFILE
[Customer's declared information]

## CASE STATUS TIMELINE
[Chronological updates with dates]

## CASE STATUS
[Current status]

## RISK ASSESSMENT
[Geographic %, Customer %, Product %, Channel %]

## NEXT STEPS
[Ordered action items]
```

**Modification Rule:** Sections locked, content within sections editable

### Template 2: STEP_0_VERIFICATION_REPORT.md
**Purpose:** Regulatory compliance evidence

**Structure (Locked):**
```markdown
# STEP 0 VERIFICATION REPORT - LOCKED TEMPLATE

## SEARCH 1-5 SECTIONS
[Each with structured findings]

## STEP 0 DECISION GATE ANALYSIS
[Summary and decision logic]

## CERTIFICATION & SIGN-OFF
[Analyst certification]
```

**Modification Rule:** Format locked, findings editable

### Template 3: AUDIT_TRAIL.md
**Purpose:** Immutable chronological log

**Structure (Fully Locked):**
```markdown
# AUDIT TRAIL - IMMUTABLE LOG

## CHRONOLOGICAL ACTION LOG
[Timestamped table of all actions]

## FINDINGS SUMMARY
[Summary of findings]

## REGULATORY COMPLIANCE NOTES
[Compliance requirements met]
```

**Modification Rule:** Auto-generated, non-editable

---

## EXCEL REPORT AUTO-GENERATION

Plugin creates professional Excel report with:

**Sheet 1: Executive Summary**
- Case ID, Customer, Date, Status
- All five searches with results
- Key findings
- Decision: PROCEED or ESCALATE

**Sheet 2: Step 0 Searches**
- Search 1-5 results in detail
- Severity assessment
- Sources documented

**Sheet 3: Discrepancies (if any)**
- Declared vs. Actual comparison
- Discrepancy analysis
- Severity levels

**Sheet 4: Risk Assessment**
- Geographic risk %
- Customer risk %
- Product risk %
- Channel risk %
- Overall risk level

---

## QUALITY ASSURANCE CHECKPOINTS

### Checkpoint 1: Step 0 Completeness
- [ ] All five searches documented
- [ ] All findings entered with sources
- [ ] Discrepancies identified
- [ ] Decision gate applied

### Checkpoint 2: Documentation Accuracy
- [ ] Case folder properly named
- [ ] Locked templates enforced
- [ ] Excel report generated
- [ ] Audit trail created

### Checkpoint 3: Regulatory Compliance
- [ ] AMLD5 Article 10 requirements met
- [ ] UK MLR Regulation 19 compliance
- [ ] FCA guidance followed
- [ ] Independent sources used

### Checkpoint 4: Decision Logic
- [ ] PROCEED decision justified
- [ ] ESCALATE decision documented
- [ ] Manager escalation routed
- [ ] Next steps clear

---

## COMMON MISTAKES TO AVOID

❌ **Mistake 1:** Accepting customer declarations without independent verification
✓ **Correct:** Complete all five searches regardless of what customer says

❌ **Mistake 2:** Skipping Step 0 for "low-risk" customers
✓ **Correct:** Step 0 is mandatory for ALL customers

❌ **Mistake 3:** Using single search instead of five
✓ **Correct:** All five searches required; each adds unique information

❌ **Mistake 4:** Modifying locked template format
✓ **Correct:** Locked templates maintain consistency; modify content, not format

❌ **Mistake 5:** Proceeding with onboarding despite critical findings
✓ **Correct:** Escalate when discrepancies found; don't override decision gate

---

## WORKFLOW DECISION TREE

```
START ONBOARDING
    ↓
CREATE CASE FOLDER
    ↓
BEGIN STEP 0
    ↓
    ┌─── SEARCH 1: ADVERSE MEDIA
    │         ↓
    │    Findings? → NO → Continue
    │         ↓ YES
    │    Document → Continue (to Search 2)
    │
    ├─── SEARCH 2: DIRECTORSHIPS
    │         ↓
    │    Findings? → NO → Continue
    │         ↓ YES
    │    Document → Continue (to Search 3)
    │
    ├─── SEARCH 3: PEP STATUS
    │         ↓
    │    PEP? → NO → Continue
    │       ↓ YES
    │    Document → Continue (to Search 4)
    │
    ├─── SEARCH 4: PROFESSIONAL BACKGROUND
    │         ↓
    │    Discrepancies? → NO → Continue
    │         ↓ YES
    │    Document → Continue (to Search 5)
    │
    └─── SEARCH 5: SANCTIONS/CRIME
             ↓
        Matches? → NO → STEP 0 COMPLETE
             ↓ YES
        IMMEDIATE ESCALATION
```

---

## STEP 0 ENFORCEMENT IN PLUGIN

**Built-In Gating:**
```
Cannot proceed past Step 0 unless:
✓ All five searches completed
✓ Report generated and signed
✓ Decision documented
✓ Escalation (if needed) routed
```

**This ensures:**
- No onboarding without independent verification
- All findings captured and documented
- Regulatory compliance automatic
- Audit trail created
- Manager review triggered for escalations

---

## SUMMARY: YOUR RESPONSIBILITIES

**As Analyst:**
1. ✓ Execute each of five searches independently
2. ✓ Document findings with sources
3. ✓ Identify discrepancies
4. ✓ Review Step 0 report
5. ✓ Follow decision gate
6. ✓ Escalate when required

**As Manager:**
1. ✓ Review escalations
2. ✓ Assess critical findings
3. ✓ Make proceed/decline/EDD decision
4. ✓ Document decision in case file
5. ✓ Sign off completion

**As Compliance:**
1. ✓ Audit case folders
2. ✓ Verify locked templates maintained
3. ✓ Review audit trails
4. ✓ Spot-check findings accuracy
5. ✓ Ensure regulatory compliance

---

**Developed by:** Vyayasan
**Version:** 1.0.0
**Date:** 12 February 2026
**Status:** Production Ready - Final Locked Version

**Stagegate Reference:** See `commands/onboard.md` for full 17-stagegate workflow specification.
**Connector Reference:** See `CONNECTORS.md` and `MCP_INTEGRATION_GUIDE.md` for MCP tool integration.
