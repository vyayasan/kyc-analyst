---
description: Customer onboarding with Step 0 verification (HITL consent required)
argument-hint: "<customer name and basic details>"
---

# Onboard

**Starting onboarding workflow...**

**Customer:** $ARGUMENTS

**IMPORTANT:** If no customer name appears above, the command failed to receive arguments. Try again with:
```
/kyc-analyst:onboard <customer name>
```

---

# STAGEGATE ENFORCEMENT - MANDATORY EXECUTION ORDER

**THIS WORKFLOW CANNOT BE BYPASSED OR REORDERED**

You MUST follow this exact sequence. Each stagegate requires explicit analyst approval before proceeding.

---

## CRITICAL: READ THIS FIRST

**DO NOT** jump straight to creating case folders or asking for customer details.

**DO NOT** start with "Perfect! I'll help you onboard..." and create folders immediately.

**DO NOT** assume the analyst has gathered customer information.

**YOU MUST** follow the stagegates below IN ORDER.

---

## STAGEGATE 1: COMMAND VERIFICATION (MANDATORY - NO SKIP)

**CHECK:** Did the command receive customer name in $ARGUMENTS?

**IF YES:**
- Customer name detected: `$ARGUMENTS`
- Proceed to Stagegate 2

**IF NO (empty or just spaces):**
```
ERROR: No customer name provided.

Usage: /kyc-analyst:onboard <customer name>

Example: /kyc-analyst:onboard Joanne Dewar UK
```

**STOP HERE** - Do not proceed until customer name is provided.

---

## STAGEGATE 2: ANALYST BRIEFING (MANDATORY - NO SKIP)

**Before creating ANY folders or files, present this briefing:**

```
========================================
KYC ANALYST v2.3.0 - ONBOARDING WORKFLOW
========================================

Customer: $ARGUMENTS

This workflow follows EU AMLD5 Article 10 mandatory independent verification.

WHAT WILL HAPPEN:

PHASE 1: Information Gathering (YOU DO THIS)
  You will gather complete customer information
  I will NOT create folders until you provide this

PHASE 2: Case Folder Creation (I DO THIS)
  I will create case folder: KYC-[DATE]-ONB-[NAME]-[SEQ]
  Numbered subfolders: 001_CASE_METADATA through 006_AUDIT_TRAIL
  Locked template files

PHASE 3: Step 0 Verification (WE DO THIS TOGETHER)
  5 mandatory searches (your explicit consent required for each)
  Decision gate analysis (PROCEED or ESCALATE)
  Professional Excel report and PDF report generation

YOUR ROLE:
  Give explicit consent for each search
  Verify all extracted data accuracy
  Make final PROCEED/ESCALATE decision

MY ROLE:
  Create case folder structure
  Automate browser searches (WITH your consent) via ~~browser
  Extract data (WITH your verification)
  Generate documentation and reports
  Save to ~~cloud storage (if connected)

========================================
ANALYST APPROVAL REQUIRED
========================================

Have you gathered the customer information required for onboarding?

Type 'ready' if you have customer details ready
Type 'gather' if you need the information checklist first
```

**STOP HERE** - Wait for analyst response: "ready" or "gather"

**DO NOT** create folders yet.
**DO NOT** ask for customer details yet.
**DO NOT** proceed until analyst responds.

---

## STAGEGATE 3: INFORMATION REQUIREMENT (CONDITIONAL)

**IF analyst typed 'gather' in Stagegate 2:**

Present this checklist:

```
========================================
CUSTOMER INFORMATION REQUIRED
========================================

You MUST gather this information from the customer BEFORE we create the case folder:

BASIC IDENTITY:
  Full legal name (as on ID)
  Date of birth
  Nationality/Nationalities
  Current residential address (full address)
  Contact details (phone, email)

EMPLOYMENT & OCCUPATION:
  Current occupation/profession
  Employer name and business
  Employment status (employed/self-employed/retired/other)
  Industry sector

BUSINESS PROFILE (CRITICAL FOR SEARCH 2):
  ALL declared directorships (company names and roles)
  Any declared business interests or investments
  Any declared shareholdings (>25% beneficial ownership)
  Any declared partnerships or sole trader businesses

FINANCIAL INFORMATION:
  Declared source of funds (for this relationship)
  Declared source of wealth (how wealth was accumulated)
  Expected account activity/transaction volumes

PURPOSE OF RELATIONSHIP:
  What products/services is the customer seeking?
  Intended use of the account/relationship

========================================

Once you have gathered this information from the customer, type 'ready' to proceed to case folder creation.
```

**STOP HERE** - Wait for analyst to type 'ready'

**DO NOT** create folders until analyst confirms 'ready'

---

**IF analyst typed 'ready' in Stagegate 2:**

Proceed directly to Stagegate 4

---

## STAGEGATE 4: CASE FOLDER CREATION (MANDATORY - NO SKIP)

**NOW create the case folder structure:**

1. **Generate case reference:**
   - Format: `KYC-[YYYYMMDD]-ONB-[LASTNAME]-[SEQ]`
   - Example: `KYC-20260206-ONB-DEWAR-001`

2. **Create base folder:**
   ```
   ~/Documents/KYC-CASES/KYC-[YYYYMMDD]-ONB-[LASTNAME]-[SEQ]/
   ```

3. **Create numbered subfolders:**
   ```
   001_CASE_METADATA/
   002_STEP_0_SEARCHES/
   003_VERIFICATION_OUTCOMES/
   004_DECISION_DOCUMENTATION/
   005_ESCALATION_BRIEF/
   006_AUDIT_TRAIL/
   ```

4. **Create locked template files:**
   - `001_CASE_METADATA/CASE_METADATA.md` (use Template A below)
   - `002_STEP_0_SEARCHES/Search_1_Findings.md` (empty, ready for Search 1)
   - `002_STEP_0_SEARCHES/Search_1.5_Findings.md` (empty, ready for ICIJ)
   - `002_STEP_0_SEARCHES/Search_2_Findings.md` (empty, ready for Search 2)
   - `002_STEP_0_SEARCHES/Search_3_Findings.md` (empty, ready for Search 3)
   - `002_STEP_0_SEARCHES/Search_4_Findings.md` (empty, ready for Search 4)
   - `002_STEP_0_SEARCHES/Search_5_Findings.md` (empty, ready for Search 5)
   - `002_STEP_0_SEARCHES/STEP_0_VERIFICATION_REPORT.md` (use Template B below)
   - `006_AUDIT_TRAIL/AUDIT_TRAIL.md` (use Template C below)

5. **Initialize audit trail with timestamp:**
   ```
   [HH:MM] Case folder created
   [HH:MM] Locked templates initialized
   ```

**After folder creation is complete, present:**

```
CASE FOLDER CREATED

Case Reference: KYC-[YYYYMMDD]-ONB-[LASTNAME]-[SEQ]
Location: ~/Documents/KYC-CASES/[folder name]/

Folder Structure:
  001_CASE_METADATA/
  002_STEP_0_SEARCHES/ (5 search finding files + ICIJ ready)
  003_VERIFICATION_OUTCOMES/
  004_DECISION_DOCUMENTATION/
  005_ESCALATION_BRIEF/
  006_AUDIT_TRAIL/

Next: Gather customer details to populate CASE_METADATA

========================================
ANALYST APPROVAL REQUIRED
========================================

Type 'continue' to provide customer details now
```

**STOP HERE** - Wait for analyst to type 'continue'

---

## STAGEGATE 5: CUSTOMER DETAILS ENTRY (MANDATORY - NO SKIP)

**Present the information collection form:**

```
========================================
CUSTOMER DETAILS ENTRY
========================================

I will now ask you for customer details to populate CASE_METADATA.md

Please provide the following information:

1. BASIC IDENTITY INFORMATION:
   - Full legal name:
   - Date of birth:
   - Nationality:
   - Current residential address:
   - Phone:
   - Email:

2. EMPLOYMENT & OCCUPATION:
   - Current occupation:
   - Employer name:
   - Employment status:
   - Industry sector:

3. DECLARED BUSINESS PROFILE:
   - Declared directorships (list all):
   - Declared business interests:
   - Declared shareholdings (>25%):
   - Declared partnerships:

4. FINANCIAL INFORMATION:
   - Declared source of funds:
   - Declared source of wealth:
   - Expected account activity:

5. PURPOSE OF RELATIONSHIP:
   - Products/services sought:
   - Intended account use:

Please provide this information now (you can paste it all at once or answer each section).
```

**STOP HERE** - Wait for analyst to provide customer information

**DO NOT** proceed until you receive customer details

---

## STAGEGATE 6: METADATA POPULATION (MANDATORY - NO SKIP)

**After receiving customer details:**

1. **Update `001_CASE_METADATA/CASE_METADATA.md`** with provided information

2. **Update audit trail:**
   ```
   [HH:MM] Customer details entered
   [HH:MM] CASE_METADATA.md populated
   ```

3. **Present confirmation:**

```
CUSTOMER DETAILS RECORDED

CASE_METADATA.md has been populated with:
  Case Reference: [reference]
  Customer Name: [name]
  Date of Birth: [dob]
  Nationality: [nationality]
  Declared Business Profile: [details]
  Expected Relationship: [details]

========================================
READY FOR STEP 0 VERIFICATION
========================================

Next: Begin 5 mandatory independent searches

Type 'begin-step-0' to start Step 0 verification
```

**STOP HERE** - Wait for analyst to type 'begin-step-0'

**DO NOT** start searches automatically

---

## STAGEGATE 7: STEP 0 COMMENCEMENT (MANDATORY - NO SKIP)

**After analyst types 'begin-step-0':**

**Update audit trail:**
```
[HH:MM] Step 0 verification commenced
```

**Present Step 0 briefing:**

```
========================================
STEP 0: MANDATORY INDEPENDENT VERIFICATION
========================================

EU AMLD5 Article 10(a) requires verification using reliable independent sources.

You MUST complete all 5 searches:

  1  SEARCH 1: Adverse Media
  1.5 SEARCH 1.5: Offshore Entities (ICIJ)
  2  SEARCH 2: Directorships (CRITICAL - catches hidden companies)
  3  SEARCH 3: PEP Status
  4  SEARCH 4: Professional Background
  5  SEARCH 5: Sanctions/Crime

HOW THIS WORKS:
  I will ask for consent before EACH search
  You type 'proceed' to authorize browser automation
  I will extract data and show you for verification
  You type 'confirm' to accept or 'redo' to re-extract
  I will document findings to Search_N_Findings.md

HUMAN-IN-THE-LOOP (HITL):
  Every search requires YOUR explicit consent
  Every data extraction requires YOUR verification
  You can type 'manual' to enter data yourself
  You can type 'skip' with documented reason

MCP TOOLS I WILL USE (with your consent):
  ~~browser (Claude in Chrome) - for web searches and data extraction
  Desktop Commander - for file management and Excel/PDF generation
  PDF Tools - for reading/analyzing PDF documents

========================================
ANALYST APPROVAL REQUIRED
========================================

Type 'start-search-1' to begin Search 1: Adverse Media
```

**STOP HERE** - Wait for analyst to type 'start-search-1'

---

## STAGEGATE 8: SEARCH 1 - ADVERSE MEDIA (MANDATORY - NO SKIP)

**After analyst types 'start-search-1':**

```
========================================
SEARCH 1: ADVERSE MEDIA
========================================

Customer: [name]

I will search for:
  Criminal records, Fraud allegations, Sanctions actions
  Regulatory findings, Negative news coverage

SOURCES (72+ DEEP SOURCES):

TIER 1: PREMIUM FINANCIAL NEWS (10 sources)
  Financial Times, Wall Street Journal, Bloomberg, Reuters, Economist
  Nikkei Asia, Financial News, Euromoney, The Banker, Global Finance

TIER 2: INVESTIGATIVE JOURNALISM (10 sources)
  ProPublica, ICIJ, Bellingcat, OCCRP, Bureau of Investigative Journalism
  The Intercept, Center for Public Integrity, OpenSecrets, FollowTheMoney
  Transparency International

TIER 3: UK/EU PREMIUM PRESS (8 sources)
  The Guardian, The Telegraph, The Times, Sunday Times, The Independent
  Evening Standard, Politico Europe, EUobserver

TIER 4: US PREMIUM PRESS (5 sources)
  New York Times, Washington Post, LA Times, Boston Globe, Chicago Tribune

TIER 5: LEGAL/REGULATORY NEWS (8 sources)
  Law360, Legal Cheek, The Lawyer, American Lawyer, MLex
  Compliance Week, AML Intelligence, Global Investigations Review

TIER 6-11: Industry, Wire Services, Archives, Leaked Data, Specialist, Government (31+ sources)

TOTAL: 72+ DEEP SOURCES

BROWSER AUTOMATION REQUIRED:
  I will use ~~browser (Claude in Chrome) to open searches
  I will read page content and extract headlines
  I will show you extracted data for verification

========================================
ANALYST CONSENT REQUIRED
========================================

Type 'proceed' to authorize browser automation for Search 1
Type 'manual' to enter findings yourself
```

**STOP HERE** - Wait for analyst response

**IF 'proceed':** Use Claude in Chrome tools to:
  1. Get browser context (`mcp__Claude_in_Chrome__tabs_context_mcp`)
  2. Create/navigate to Google News
  3. Search for "[customer name] adverse media"
  4. Extract headlines and dates
  5. Repeat for BBC, Reuters, FT
  6. Show extracted data to analyst

**Present extracted data:**
```
========================================
SEARCH 1: EXTRACTED DATA
========================================

SOURCE: Google News
HEADLINES FOUND:
  "[headline 1]" - [source], [date]
  "[headline 2]" - [source], [date]

SOURCE: BBC News
HEADLINES FOUND:
  [none] OR [list headlines]

========================================
ANALYST VERIFICATION REQUIRED
========================================

Type 'confirm' if data is accurate
Type 'redo' to re-extract data
Type 'edit' to manually correct data
```

**STOP HERE** - Wait for analyst verification

**After 'confirm':**
  1. Write findings to `002_STEP_0_SEARCHES/Search_1_Findings.md`
  2. Update audit trail: `[HH:MM] Search 1 completed - Adverse Media`
  3. Present: `SEARCH 1 COMPLETE - Findings documented`

**IF 'manual':** Ask analyst to provide findings, then document

---

## STAGEGATE 8.5: SEARCH 1.5 - OFFSHORE ENTITIES (ICIJ)

**Automatically present after Search 1 complete:**

```
========================================
SEARCH 1.5: OFFSHORE ENTITIES (LEAKED DATA)
========================================

Customer: [name]

EXCLUSIVE DATA - Not available on LexisNexis, Dow Jones, or Refinitiv
ICIJ Offshore Leaks is FREE public data from investigative journalism

I will search for:
  Offshore company ownership, Shell companies and tax havens
  Leaked financial records, Beneficial ownership structures

SOURCES (4 ICIJ DATABASES):
  ICIJ Panama Papers - 11.5M leaked documents from Mossack Fonseca (2016)
  ICIJ Paradise Papers - 13.4M leaked files, Appleby offshore structures (2017)
  ICIJ Pandora Papers - 11.9M leaked records from 14 offshore providers (2021)
  ICIJ Offshore Leaks Database - 810,000+ offshore entities (consolidated search)

========================================
ANALYST CONSENT REQUIRED
========================================

Type 'proceed' to authorize browser automation for Search 1.5
Type 'skip' if customer has NO offshore connections (low risk profile)
Type 'manual' to enter findings yourself
```

**STOP HERE** - Wait for analyst response

**After search execution, present findings and wait for 'confirm'**
**After 'confirm':** Write to Search_1.5_Findings.md, update audit trail

---

## STAGEGATE 9: SEARCH 2 - DIRECTORSHIPS (MANDATORY - NO SKIP - CRITICAL)

**Automatically present after Search 1.5 complete:**

```
========================================
SEARCH 2: DIRECTORSHIPS (CRITICAL SEARCH)
========================================

Customer: [name]

This search is CRITICAL for catching undisclosed business interests.

I will search for:
  ALL company directorships (current and resigned)
  Hidden companies not declared by customer
  Shareholdings and beneficial ownership

SOURCES:
  Companies House: Officer search for "[name]"
  Companies House: Company search for "[name]"
  Business registries and directories

WHAT I'M LOOKING FOR:
  Compare found companies vs. declared companies
  Identify UNDISCLOSED directorships
  Flag material misrepresentation patterns

========================================
ANALYST CONSENT REQUIRED
========================================

Type 'proceed' to authorize browser automation for Search 2
Type 'manual' to enter findings yourself
```

**STOP HERE** - Wait for analyst response

**IF 'proceed':** Use ~~browser to navigate Companies House, extract directorships
**Present data, wait for 'confirm'**
**After 'confirm':** Write to Search_2_Findings.md, update audit trail

---

## STAGEGATE 10: SEARCH 3 - PEP STATUS (MANDATORY - NO SKIP)

```
========================================
SEARCH 3: PEP STATUS
========================================

SOURCES (5 EXPLICIT PEP DATABASES):
  EveryPolitician.org - 233 countries
  Wikidata SPARQL - Structured political positions
  UK Parliament Members API - MPs, Lords, officials
  Register of Members' Interests - UK political interests
  CIA World Leaders - Global government officials

========================================
ANALYST CONSENT REQUIRED
========================================

Type 'proceed' to authorize Search 3
Type 'manual' to enter findings yourself
```

**STOP HERE** - Wait for analyst response, execute, present, wait for 'confirm'

---

## STAGEGATE 11: SEARCH 4 - PROFESSIONAL BACKGROUND (MANDATORY - NO SKIP)

```
========================================
SEARCH 4: PROFESSIONAL BACKGROUND
========================================

SOURCES:
  LinkedIn profile search
  Company websites (employer verification)
  Business news mentions
  Trade publications
  Professional directories

========================================
ANALYST CONSENT REQUIRED
========================================

Type 'proceed' to authorize Search 4
Type 'manual' to enter findings yourself
```

**STOP HERE** - Wait for analyst response, execute, present, wait for 'confirm'

---

## STAGEGATE 12: SEARCH 5 - SANCTIONS/CRIME (MANDATORY - NO SKIP)

```
========================================
SEARCH 5: SANCTIONS/CRIME
========================================

SOURCES (12 SANCTIONS + LEGAL SOURCES):

TIER 1: SANCTIONS LISTS (6 sources)
  OpenSanctions.org - Aggregates 30+ sanctions lists
  OFAC SDN List - US Treasury sanctions
  OFSI - UK Treasury sanctions
  EU Consolidated List - European Union sanctions
  UN Security Council List - United Nations sanctions
  Interpol Red Notices - International arrest warrants

TIER 3: LEGAL/REGULATORY DATABASES (6 sources - UK focused)
  BAILII - British & Irish Legal Information Institute
  Courts.gov.uk - UK court records
  Insolvency Service - IVAs, bankruptcies
  Disqualified Directors Register - Companies House
  London Gazette - Official public record
  FCA Warning List - Unauthorized firms

========================================
ANALYST CONSENT REQUIRED
========================================

Type 'proceed' to authorize Search 5
Type 'manual' to enter findings yourself
```

**STOP HERE** - Wait for analyst response, execute, present, wait for 'confirm'

---

## STAGEGATE 13: STEP 0 VERIFICATION REPORT (MANDATORY - NO SKIP)

**Automatically present after all searches complete:**

```
========================================
STEP 0: ALL SEARCHES COMPLETE
========================================

All mandatory searches have been completed:

  Search 1: Adverse Media
  Search 1.5: Offshore Entities (ICIJ)
  Search 2: Directorships
  Search 3: PEP Status
  Search 4: Professional Background
  Search 5: Sanctions/Crime

Next: I will compile the STEP_0_VERIFICATION_REPORT.md

This report includes:
  Summary of all search results
  Detailed findings from each search
  Comparison of declared vs. verified information
  Identification of discrepancies
  Heuristic Risk Scoring (automatic four-factor model)
  Decision Gate Analysis (PROCEED or ESCALATE)

========================================
ANALYST APPROVAL REQUIRED
========================================

Type 'compile-report' to generate STEP_0_VERIFICATION_REPORT
```

**STOP HERE** - Wait for analyst to type 'compile-report'

**After 'compile-report':**

1. Compile all findings into STEP_0_VERIFICATION_REPORT.md
2. Calculate heuristic risk score using four-factor model:
   - Geographic Risk (30%): Customer jurisdiction, transaction countries
   - Customer Risk (35%): PEP, industry, source of wealth, complexity
   - Product Risk (25%): Account type, expected activity
   - Channel Risk (10%): Onboarding method, documentation quality
   Total = (Geographic x 0.30) + (Customer x 0.35) + (Product x 0.25) + (Channel x 0.10)
   Bands: LOW (0-20), MEDIUM (21-60), HIGH (61-80), CRITICAL (81-100)

3. Present decision gate with risk score and ask analyst to approve

```
DECISION: [PROCEED / ESCALATE]

Do you agree with this decision?

Type 'approve-decision' to confirm
Type 'revise' to modify decision rationale
```

**STOP HERE** - Wait for analyst approval

---

## STAGEGATE 14: ESCALATION PROCESSING (CONDITIONAL)

**IF decision = ESCALATE:**
Prepare ESCALATION_BRIEF.md in 005_ESCALATION_BRIEF/
Present escalation and wait for 'prepare-escalation' consent

**IF decision = PROCEED:**
Skip to Stagegate 15

---

## STAGEGATE 15: EXCEL REPORT GENERATION (MANDATORY - NO SKIP)

```
========================================
EXCEL REPORT GENERATION
========================================

I will generate the professional 4-sheet Excel report:

SHEET 1: Executive Summary
SHEET 2: Directorships
SHEET 3: Discrepancies
SHEET 4: Risk Assessment

========================================
ANALYST APPROVAL REQUIRED
========================================

Type 'generate-excel' to create Excel report
```

**STOP HERE** - Wait for 'generate-excel'

**After 'generate-excel':**
1. Create Excel using openpyxl (Python) with professional formatting
2. Save as: `KYC-[DATE]-ONB-[NAME]-[SEQ]_Report.xlsx`
3. Update audit trail
4. Present confirmation

---

## STAGEGATE 16: PDF REPORT GENERATION (RECOMMENDED)

```
========================================
PDF REPORT GENERATION
========================================

I will generate the 17-section professional PDF report.

Sections include:
  Title banner, Customer details, Executive summary
  All search results (1, 1.5, 2, 3, 4, 5)
  Discrepancy analysis, Decision gate, Risk assessment
  Compliance statement, Regulatory basis, Deliverables
  Next steps, Approvals (Analyst/Manager/MLRO)

========================================
ANALYST APPROVAL REQUIRED
========================================

Type 'generate-pdf' to create PDF report
Type 'skip-pdf' to proceed with Excel only
```

**STOP HERE** - Wait for response

**After 'generate-pdf':**
1. Generate PDF using fpdf2 (Python) with professional formatting
2. Save as: `KYC-[DATE]-ONB-[NAME]-[SEQ]-Step0-Report.pdf`
3. Update audit trail
4. Present confirmation and proceed to finalization

**IF 'skip-pdf':** Skip to STAGEGATE 17

---

## STAGEGATE 17: CASE FINALIZATION (MANDATORY - NO SKIP)

1. **Perform final QA checklist:**
   - All 5+ searches completed
   - All findings documented
   - CASE_METADATA complete
   - STEP_0_VERIFICATION_REPORT complete
   - Decision gate analysis complete
   - Excel report generated
   - PDF report generated (if applicable)
   - Audit trail complete
   - Case folder structure correct (001-006)

2. **Update audit trail with completion**

3. **Present final summary:**

```
========================================
ONBOARDING WORKFLOW COMPLETE
========================================

Case Reference: KYC-[DATE]-ONB-[NAME]-[SEQ]

COMPLETED:
  Case folder created with 001-006 structure
  Customer details gathered and documented
  Step 0: All mandatory searches completed
  Step 0 Verification Report compiled
  Decision Gate Analysis: [PROCEED/ESCALATE]
  Excel report generated (4 sheets)
  PDF report generated (17 sections)
  Audit trail complete and immutable
  Quality assurance checklist verified

DELIVERABLES:
  Case Folder: ~/Documents/KYC-CASES/[case folder]/
  Verification Report: 002_STEP_0_SEARCHES/STEP_0_VERIFICATION_REPORT.md
  Excel Report: KYC-[DATE]-ONB-[NAME]-[SEQ]_Report.xlsx
  PDF Report: KYC-[DATE]-ONB-[NAME]-[SEQ]-Step0-Report.pdf
  Audit Trail: 006_AUDIT_TRAIL/AUDIT_TRAIL.md

DECISION: [PROCEED / ESCALATE]

REGULATORY COMPLIANCE CONFIRMED:
  EU AMLD5 Article 10 - Independent verification completed
  UK MLR 2017 Regulation 19 - Customer information verified
  FCA Guidance - Robust CDD procedures applied
  Locked template formats maintained
  Full audit trail documented with HITL consents

========================================
END OF ONBOARDING WORKFLOW
========================================

Cost savings: 563-943 per case (99.7% reduction vs LexisNexis/Dow Jones/Refinitiv)
Database coverage: 90+ sources (72+ adverse media, 5 PEP, 12 sanctions/legal, 4 ICIJ offshore)
```

---

# STAGEGATE ENFORCEMENT SUMMARY

**THIS WORKFLOW REQUIRES:**

17 mandatory stagegates in sequence
Explicit analyst approval at each gate
No skipping or reordering
HITL consent for all searches
Verification of all extracted data
Locked template formats
Immutable audit trail
Professional Excel dashboard
Professional PDF report

**CANNOT PROCEED WITHOUT:**
Customer name in command
Analyst confirming information gathered
Case folder creation
Customer details entry
All 5+ searches completed
Step 0 verification report
Decision gate analysis
Excel report generation

---

# TEMPLATES

## TEMPLATE A: CASE_METADATA.md

```markdown
# Case Metadata - [Case Reference]

**Format: LOCKED** - Structure cannot be modified

---

## Case Identification

**Case Reference:** KYC-[YYYYMMDD]-ONB-[LASTNAME]-[SEQ]
**Case Type:** Customer Onboarding
**Created:** [Date and Time]
**Analyst:** [Analyst Name]
**Status:** [IN PROGRESS / COMPLETED / ESCALATED]

---

## Customer Details

**Full Legal Name:** [As appears on ID]
**Date of Birth:** [DD/MM/YYYY]
**Nationality:** [Nationality/Nationalities]
**Current Residential Address:** [Full Address]
**Contact Phone:** [Phone Number]
**Contact Email:** [Email Address]

---

## Employment & Occupation

**Current Occupation:** [Occupation/Profession]
**Employer Name:** [Company Name]
**Employment Status:** [Employed/Self-Employed/Retired/Other]
**Industry Sector:** [Sector]

---

## Declared Business Profile

**Declared Directorships:**
- [Company Name 1] - [Role] - [Status]
- [OR: None declared]

**Declared Business Interests:**
- [Business Interest 1]
- [OR: None declared]

**Declared Shareholdings (>25%):**
- [Company Name] - [Percentage]
- [OR: None declared]

---

## Financial Information

**Declared Source of Funds:** [Description]
**Declared Source of Wealth:** [Description]
**Expected Account Activity:** [Transaction volumes, frequency]

---

## Purpose of Relationship

**Products/Services Sought:** [What customer is seeking]
**Intended Account Use:** [How customer intends to use account]

---

## Initial Risk Assessment

**Geographic Risk:** [LOW/MEDIUM/HIGH] - [Rationale]
**Customer Risk:** [LOW/MEDIUM/HIGH] - [Rationale]
**Product Risk:** [LOW/MEDIUM/HIGH] - [Rationale]
**Channel Risk:** [LOW/MEDIUM/HIGH] - [Rationale]

**Overall Initial Risk Rating:** [LOW/MEDIUM/HIGH]

---

**Last Updated:** [Date and Time]
```

---

## TEMPLATE B: STEP_0_VERIFICATION_REPORT.md

[Use the locked template from OUTPUT_TEMPLATES/PDF_Report_Template.md - 17 sections]

---

## TEMPLATE C: AUDIT_TRAIL.md

```markdown
# Audit Trail - [Case Reference]

**Format: FULLY IMMUTABLE** - Cannot be modified after entry

---

## Case Identification

**Case Reference:** KYC-[YYYYMMDD]-ONB-[LASTNAME]-[SEQ]
**Customer Name:** [Full Name]
**Audit Trail Created:** [Date and Time]

---

## Chronological Activity Log

**All timestamps are in local time and cannot be altered**

[HH:MM] Case folder created
[HH:MM] Locked templates initialized
[HH:MM] Customer details entered
[HH:MM] CASE_METADATA.md populated
[HH:MM] Step 0 verification commenced
[HH:MM] Search 1 commenced - Adverse Media
[HH:MM] Search 1 completed - Adverse Media
[HH:MM] Search 1.5 commenced - Offshore Entities (ICIJ)
[HH:MM] Search 1.5 completed - Offshore Entities (ICIJ)
[HH:MM] Search 2 commenced - Directorships
[HH:MM] Search 2 completed - Directorships
[HH:MM] Search 3 commenced - PEP Status
[HH:MM] Search 3 completed - PEP Status
[HH:MM] Search 4 commenced - Professional Background
[HH:MM] Search 4 completed - Professional Background
[HH:MM] Search 5 commenced - Sanctions/Crime
[HH:MM] Search 5 completed - Sanctions/Crime
[HH:MM] Step 0 verification report compiled
[HH:MM] Decision gate analysis completed
[HH:MM] Decision made: [PROCEED/ESCALATE]
[HH:MM] Excel report generated
[HH:MM] PDF report generated
[HH:MM] Case finalization commenced
[HH:MM] Quality assurance checklist verified
[HH:MM] All templates locked and complete
[HH:MM] Onboarding workflow complete

---

**Audit Trail Status:** COMPLETE AND LOCKED
```

---

**Version:** 2.3.0
**Author:** Vyayasan

---

END OF ONBOARDING WORKFLOW
