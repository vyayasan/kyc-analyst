# MCP Integration Guide - KYC Analyst Plugin v2.3.0

**Comprehensive guide to all free MCP integrations used in this plugin.**

**Author:** Vyayasan
**Version:** 2.3.0
**Last Updated:** February 2026

---

## Table of Contents

1. [Available MCP Tools](#available-mcp-tools)
2. [KYC Workflow Integration Examples](#kyc-workflow-integration-examples)
3. [HITL Consent Pattern with MCPs](#hitl-consent-pattern-with-mcps)
4. [Excel Dashboard Templates](#excel-dashboard-templates)
5. [PDF Generation](#pdf-generation)
6. [Important Notes and Known Issues](#important-notes-and-known-issues)

---

## Available MCP Tools

This plugin leverages four free MCP tool categories. No paid subscriptions or API keys are required. All tools operate locally and are invoked through Claude Code / Cowork.

---

### 1. Claude in Chrome (Browser Automation)

**Purpose:** Web research for Step 0 independent verification searches. Enables automated browsing of Companies House, news sites, sanctions lists, LinkedIn, and other public sources.

**MCP Server:** Built into Claude Code Chrome extension (no configuration needed).

| Tool | Description | KYC Use Case |
|------|-------------|--------------|
| `tabs_context_mcp` | Get browser context and list of active tabs in the MCP group | Initialise browser session before any web research |
| `tabs_create_mcp` | Create a new empty tab in the MCP tab group | Open dedicated tabs for each Step 0 search |
| `navigate` | Navigate to a URL or go forward/back in browser history | Navigate to Companies House, OFAC, news sites |
| `read_page` | Get accessibility tree representation of page elements | Parse structured data from registry results |
| `get_page_text` | Extract raw text content from the page | Capture article text, search results, registry entries |
| `find` | Find elements by natural language description | Locate search boxes, result links, form fields |
| `form_input` | Set values in form elements using element references | Enter customer names into search fields |
| `computer` | Mouse clicks, keyboard input, screenshots, scrolling | Click search buttons, capture evidence screenshots |

**Tab Management Flow:**
```
1. tabs_context_mcp    --> Get or create tab group
2. tabs_create_mcp     --> Create tab for this search
3. navigate            --> Go to target site (e.g., Companies House)
4. find / read_page    --> Locate the search input
5. form_input          --> Enter customer name
6. computer (click)    --> Submit the search
7. get_page_text       --> Extract results
8. computer (screenshot) --> Capture evidence screenshot
```

---

### 2. Desktop Commander (File Management)

**Purpose:** Create all case outputs -- case folders, Excel dashboards, PDF reports, audit trails, evidence files. This is the primary output engine for the plugin.

**MCP Server:** Desktop Commander (free, local install).

| Tool | Description | KYC Use Case |
|------|-------------|--------------|
| `write_file` | Create files (text, Excel via JSON, CSV) | Generate Excel dashboards, audit trails, case metadata, evidence files |
| `read_file` | Read file contents | Read existing case files, templates, previous audit trails |
| `create_directory` | Create folders and nested directory structures | Create the 7 mandatory case subfolders (00-06) |
| `list_directory` | List files in a directory | Verify case folder structure, list evidence files |
| `write_pdf` | Create PDF from markdown content | Generate the 17-section PDF verification report |

**File Creation Capabilities:**

| File Type | Method | Notes |
|-----------|--------|-------|
| `.xlsx` (Excel) | `write_file` with JSON content | Multi-sheet dashboards; content must be valid JSON |
| `.pdf` (PDF) | `write_pdf` with markdown content | Converts markdown to styled PDF |
| `.md` (Markdown) | `write_file` with text content | Locked templates (CASE_METADATA, STEP_0_REPORT, AUDIT_TRAIL) |
| `.txt` (Text) | `write_file` with text content | Audit trails, evidence indexes |
| `.csv` (CSV) | `write_file` with CSV content | Data exports, screening summaries |

---

### 3. PDF Tools (Analysis)

**Purpose:** Read and analyse existing PDF documents submitted by customers or generated during previous KYC reviews.

**MCP Server:** PDF Tools - Analyze, Extract, Fill, Compare (free).

| Tool | Description | KYC Use Case |
|------|-------------|--------------|
| `read_pdf_content` | Extract full text content from a PDF file | Read customer-submitted ID documents, previous KYC reports, regulatory notices |
| `read_pdf_fields` | Read form field names and values from a PDF | Extract data from structured PDF forms (e.g., application forms, declarations) |

**Typical Usage:**
```
1. Customer submits application as PDF
2. read_pdf_content --> Extract all text from the PDF
3. Parse customer details (name, DOB, address, occupation)
4. Feed extracted data into Step 0 verification searches
```

---

### 4. Control Chrome (Tab Management)

**Purpose:** Supplementary browser control for managing Chrome tabs outside the MCP tab group. Useful for switching between research tabs and reading page content.

**MCP Server:** Control Chrome (free).

| Tool | Description | KYC Use Case |
|------|-------------|--------------|
| `open_url` | Open a URL in Chrome (new tab or current) | Quick-open reference sites, regulatory pages |
| `get_current_tab` | Get information about the active tab | Verify which page is currently active |
| `list_tabs` | List all open tabs in Chrome | Overview of all open research tabs |
| `switch_to_tab` | Switch to a specific tab by ID | Navigate between multiple search results |
| `get_page_content` | Get text content of the current page | Alternative text extraction method |

---

## KYC Workflow Integration Examples

These examples show how MCP tools combine to execute real KYC workflows. Each example includes the HITL consent checkpoints required by the plugin.

---

### Example 1: Adverse Media Search with Evidence Capture

**Step 0, Search 1** -- Uses Claude in Chrome to search 72+ adverse media sources and capture evidence.

```
WORKFLOW: Adverse Media Search for "John Smith"
MCP TOOLS USED: Claude in Chrome, Desktop Commander

Step 1: [HITL] Ask analyst: "Shall I proceed with Search 1: Adverse Media
        for John Smith across 72+ sources?"
        --> Wait for "yes" / "proceed"

Step 2: tabs_context_mcp
        --> Get browser context, identify available tabs

Step 3: tabs_create_mcp
        --> Create new tab for adverse media research

Step 4: navigate --> https://www.google.com/search?q="John+Smith"+fraud+crime+scandal&tbm=nws
        --> Google News search for adverse media

Step 5: get_page_text
        --> Extract search results text

Step 6: computer (action: screenshot)
        --> Capture screenshot of search results page

Step 7: write_file --> /Cases/2026/Smith_John_20260211/00_Step0_Verification/
                       Screenshots/Adverse_Media_Search_20260211.png
        --> Save evidence screenshot to case folder

Step 8: Repeat Steps 4-7 for BBC, Reuters, FCA Register, Companies House,
        court records, insolvency register (rotate through sources)

Step 9: write_file --> /Cases/2026/Smith_John_20260211/00_Step0_Verification/
                       Evidence/News_Articles/Search_1_Findings.md
        --> Document all findings in structured markdown

Step 10: [HITL] Present findings to analyst:
         "Search 1 Complete. Result: CLEAR. No adverse media found across
          72+ sources. 2 false positives reviewed and excluded (different
          individuals). Confirm this result?"
         --> Wait for analyst confirmation
```

---

### Example 2: Companies House Directorship Extraction

**Step 0, Search 2** -- Uses Claude in Chrome to search Companies House for undisclosed directorships.

```
WORKFLOW: Directorship Search for "John Smith" (DOB: 15/03/1985)
MCP TOOLS USED: Claude in Chrome, Desktop Commander

Step 1: [HITL] Ask analyst: "Shall I proceed with Search 2: Directorships?
        I will search Companies House for all company directorships held by
        John Smith."
        --> Wait for "yes" / "proceed"

Step 2: tabs_create_mcp
        --> Create new tab for Companies House

Step 3: navigate --> https://find-and-update.company-information.service.gov.uk/
        --> Navigate to Companies House officer search

Step 4: find (query: "search for officers")
        --> Locate the officer search input field

Step 5: form_input (ref: [search_field_ref], value: "John Smith")
        --> Enter customer name in search field

Step 6: computer (action: left_click, coordinate: [search_button])
        --> Click the search button

Step 7: get_page_text
        --> Extract officer search results

Step 8: computer (action: screenshot)
        --> Capture evidence screenshot of results

Step 9: For each directorship found:
        - navigate to company page
        - get_page_text (extract company details, status, appointment date)
        - computer (screenshot) for evidence

Step 10: write_file --> Search_2_Findings.md
         --> Document all directorships with:
             Company Name | Position | Status | Appointment Date | Disclosed?

Step 11: [HITL] Present findings to analyst:
         "Search 2 Complete. Found 0 active directorships, 0 historical
          directorships. Customer declared no directorships -- this is
          CONSISTENT. Result: CLEAR. Confirm?"
         --> Wait for analyst confirmation

         OR (if discrepancies found):

         "Search 2 Complete. Found 2 active directorships NOT DISCLOSED
          by customer:
          1. ABC Trading Ltd (Director since 2019, ACTIVE)
          2. XYZ Holdings Ltd (Director since 2022, ACTIVE)
          DISCREPANCY: Customer declared no directorships.
          Recommendation: ESCALATE for material misrepresentation.
          Confirm escalation?"
         --> Wait for analyst decision
```

---

### Example 3: Complete Step 0 with Dashboard and PDF Generation

**Full onboarding workflow** -- All 5 searches followed by Excel dashboard and PDF report generation.

```
WORKFLOW: Complete Step 0 Verification + Output Generation
MCP TOOLS USED: Claude in Chrome, Desktop Commander, PDF Tools

PHASE 1: CASE FOLDER CREATION (Desktop Commander)
---------------------------------------------------
Step 1: [HITL] "I will create case folder KYC-20260211-ONB-SMITH-001 with
        all 7 mandatory subfolders. Proceed?"
        --> Wait for "yes"

Step 2: create_directory --> KYC_Cases/2026/02_February/Smith_John_20260211/
        create_directory --> .../00_Step0_Verification/Screenshots/
        create_directory --> .../00_Step0_Verification/Evidence/News_Articles/
        create_directory --> .../00_Step0_Verification/Evidence/Companies_House/
        create_directory --> .../00_Step0_Verification/Evidence/PEP_Documents/
        create_directory --> .../00_Step0_Verification/Evidence/Professional_Verification/
        create_directory --> .../00_Step0_Verification/Evidence/Sanctions_Evidence/
        create_directory --> .../01_Customer_Documents/
        create_directory --> .../02_Risk_Assessment/
        create_directory --> .../03_Screening_Results/
        create_directory --> .../04_Approvals/
        create_directory --> .../05_Ongoing_Monitoring/
        create_directory --> .../06_Correspondence/

Step 3: write_file --> .../CASE_METADATA.md (locked template populated)

PHASE 2: STEP 0 SEARCHES (Claude in Chrome)
---------------------------------------------------
Step 4-8: Execute Searches 1-5 (see Examples 1 and 2 above)
          Each search: [HITL consent] --> Execute --> [HITL confirm result]

PHASE 3: EXCEL DASHBOARD (Desktop Commander)
---------------------------------------------------
Step 9: [HITL] "All 5 Step 0 searches complete. Results:
        Search 1 (Adverse Media): CLEAR
        Search 2 (Directorships): CLEAR
        Search 3 (PEP Status): NOT PEP
        Search 4 (Professional): VERIFIED
        Search 5 (Sanctions): CLEAR
        Risk Score: 13/100 (LOW)
        Decision: PROCEED

        Shall I generate the 4-sheet Excel dashboard?"
        --> Wait for "yes"

Step 10: write_file --> KYC_Smith_John_Findings_Report.xlsx
         Content: JSON with 4 sheets (see Excel Dashboard Templates below)

PHASE 4: PDF REPORT (Desktop Commander)
---------------------------------------------------
Step 11: [HITL] "Shall I generate the 17-section PDF verification report?"
         --> Wait for "yes"

Step 12: write_pdf --> Step0_Report_JS_20260211.pdf
         Content: Markdown following the locked PDF report template

PHASE 5: AUDIT TRAIL (Desktop Commander)
---------------------------------------------------
Step 13: write_file --> Audit_Trail.txt
         Content: Immutable chronological log of all events with timestamps
```

---

### Example 4: Audit Trail Management

**Audit trail creation and evidence indexing** -- Uses Desktop Commander to build the immutable compliance record.

```
WORKFLOW: Audit Trail Generation
MCP TOOLS USED: Desktop Commander

Step 1: After each Step 0 search completes, append to audit trail:
        write_file --> Audit_Trail.txt (append mode)

        Entry format:
        ================================================================
        EVENT [N]: [EVENT TYPE]
        ================================================================
        Date/Time: [DD Month YYYY, HH:MM:SS UTC]
        Event Type: [SEARCH RESULT / DECISION GATE / APPROVAL]
        Event ID: EVT-[YYYYMMDD]-[SEQ]
        Authority: [System / Analyst ID]
        Status: [COMPLETE / CLEAR / FINDINGS / ESCALATED]

        Details:
        - [Structured findings]

        System Log Entry:
        [HH:MM:SS] [Action description]
        ================================================================

Step 2: After all searches complete, generate Evidence_Index.txt:
        write_file --> Evidence_Index.txt

        Lists every file in the case folder with:
        - File name
        - File type
        - Date created
        - Purpose
        - Location in case folder

Step 3: Lock the audit trail:
        Final entry records trail generation, hash, and immutability status.

        Trail Status: LOCKED & IMMUTABLE
        Retention Period: 5 years
```

---

## HITL Consent Pattern with MCPs

Every MCP tool invocation requires explicit Human-in-the-Loop (HITL) consent. The plugin enforces three consent patterns depending on the tool category.

---

### Pattern 1: Browser Automation Consent

**Used for:** All Claude in Chrome operations (web searches, form filling, screenshots).

```
CONSENT FLOW:

1. ASK PERMISSION TO SEARCH
   "I will now perform Search [N]: [Search Name] for [Customer Name].
    This involves navigating to [Site] and searching for [terms].
    Shall I proceed?"
   --> Wait for: "yes" / "proceed" / "go ahead"

2. EXECUTE THE SEARCH
   - Navigate to site
   - Enter search terms
   - Extract results
   - Capture screenshots

3. PRESENT FINDINGS
   "Search [N] complete. Here are the findings:
    [Structured summary of results]
    Result: [CLEAR / FINDINGS / MATCH]"

4. ASK FOR CONFIRMATION
   "Do you confirm this result? Should I record it as [CLEAR/FINDINGS]
    and proceed to Search [N+1]?"
   --> Wait for: "confirmed" / "yes, proceed"
```

**Important:** Never auto-proceed between searches. Each search requires its own consent cycle.

---

### Pattern 2: File Operations Consent

**Used for:** All Desktop Commander write operations (saving evidence, creating folders).

```
CONSENT FLOW:

1. ASK PERMISSION TO SAVE
   "I have captured [description] from [source].
    Shall I save this as evidence to:
    [full file path]?"
   --> Wait for: "yes" / "save it"

2. EXECUTE THE SAVE
   - write_file with the evidence content
   - Confirm file was written successfully

3. CONFIRM SAVE
   "Evidence saved to [path]. File size: [X KB].
    Continuing with [next action]."
```

**Note:** Case folder creation (create_directory) also requires consent before execution.

---

### Pattern 3: Report Generation Consent

**Used for:** Excel dashboard and PDF report generation.

```
CONSENT FLOW:

1. SUMMARISE WHAT WILL BE GENERATED
   "All Step 0 searches are complete. I can now generate:
    - 4-sheet Excel Dashboard (Executive Summary, Directorships,
      Discrepancies, Risk Assessment)
    - 17-section PDF Report (professional, client-ready format)
    - Audit Trail (immutable chronological log)

    Shall I generate the Excel dashboard?"
   --> Wait for: "yes" / "generate"

2. GENERATE THE FILE
   - write_file (Excel) or write_pdf (PDF)
   - Use locked template format

3. CONFIRM GENERATION
   "Excel dashboard generated:
    [full file path]
    4 sheets: Executive Summary, Directorships, Discrepancies, Risk Assessment

    Shall I now generate the PDF report?"
   --> Wait for: "yes"

4. GENERATE NEXT FILE
   - Repeat for each output file
```

---

## Excel Dashboard Templates

The plugin generates 4-sheet Excel dashboards using Desktop Commander's `write_file` tool. The content must be passed as a valid JSON structure.

### Multi-Sheet JSON Format

```json
{
  "sheets": [
    {
      "name": "Executive Summary",
      "data": [
        ["FIELD", "VALUE"],
        ["Case ID", "KYC-20260211-ONB-SMITH-001"],
        ["Customer Name", "John Smith"],
        ["Date of Birth", "15/03/1985"],
        ["Nationality", "British"],
        ["Application Date", "10/02/2026"],
        ["Onboarding Status", "PROCEED"],
        ["Risk Rating", "LOW"],
        ["Risk Score", "13/100"],
        [""],
        ["STEP 0 VERIFICATION RESULTS"],
        ["Search", "Result", "Findings"],
        ["1. Adverse Media", "CLEAR", "No adverse media found"],
        ["2. Directorships", "CLEAR", "No directorships identified"],
        ["3. PEP Status", "NOT PEP", "Not politically exposed"],
        ["4. Professional Background", "VERIFIED", "Employment confirmed"],
        ["5. Sanctions/Crime", "CLEAR", "No sanctions matches"],
        [""],
        ["DECISION"],
        ["Decision Gate", "PROCEED"],
        ["Approval", "APPROVED"],
        ["Approved By", "[Analyst Name]"],
        ["Approval Date", "11/02/2026"]
      ]
    },
    {
      "name": "Directorships",
      "data": [
        ["COMPANY NAME", "POSITION", "STATUS", "APPOINTED", "RESIGNED", "DISCLOSED"],
        ["(No directorships found)", "", "", "", "", ""],
        [""],
        ["DISCLOSURE ASSESSMENT"],
        ["Customer Declaration", "No directorships"],
        ["Verified Result", "No directorships found"],
        ["Discrepancy", "NONE - Consistent"]
      ]
    },
    {
      "name": "Discrepancies",
      "data": [
        ["CATEGORY", "DECLARED", "VERIFIED", "STATUS", "SEVERITY"],
        ["Employment", "Senior Software Engineer at TechCorp", "Confirmed via LinkedIn and company site", "CONSISTENT", "N/A"],
        ["Directorships", "None", "None found", "CONSISTENT", "N/A"],
        ["PEP Status", "Not PEP", "Not PEP (5 databases checked)", "CONSISTENT", "N/A"],
        ["Address", "42 Riverside Avenue, Manchester", "Confirmed via council tax bill", "CONSISTENT", "N/A"],
        [""],
        ["OVERALL DISCREPANCY ASSESSMENT: NONE - All declarations verified"]
      ]
    },
    {
      "name": "Risk Assessment",
      "data": [
        ["RISK FACTOR", "WEIGHT", "SCORE", "WEIGHTED SCORE"],
        ["Geographic Risk", "30%", "10/100", "3.0"],
        ["Customer Risk", "35%", "15/100", "5.25"],
        ["Product Risk", "25%", "15/100", "3.75"],
        ["Channel Risk", "10%", "10/100", "1.0"],
        ["TOTAL", "100%", "", "13.0"],
        [""],
        ["RISK BAND: LOW (0-20)"],
        ["FINAL RATING: LOW RISK"],
        [""],
        ["MONITORING REQUIREMENTS"],
        ["Review Frequency", "Annual"],
        ["Next Review", "11/02/2027"],
        ["EDD Required", "No"],
        ["Enhanced Monitoring", "Not required"]
      ]
    }
  ]
}
```

### Key Rules for Excel Generation

1. **Content must be valid JSON** -- Malformed JSON will cause `write_file` to fail silently or produce a corrupt file.
2. **Each sheet is an object** with `name` (string) and `data` (array of arrays).
3. **Empty rows** use `[""]` to create visual spacing between sections.
4. **No formulas** -- All values must be plain strings or numbers. Excel formulas are not supported through this method.
5. **File extension must be `.xlsx`** -- Desktop Commander infers the format from the extension.

---

## PDF Generation

The plugin generates professional 17-section PDF reports. Two methods are available.

### Method 1: Desktop Commander `write_pdf` (Preferred)

Converts markdown content directly to a styled PDF. This is the recommended approach for the Step 0 Verification Report.

```
Tool: write_pdf
Input: Markdown content following the locked PDF report template
Output: Professional PDF with:
  - Title banner with gradient styling
  - Customer details table
  - Executive summary
  - All 5 Step 0 search results
  - Decision gate analysis
  - Risk assessment
  - Compliance statement
  - Approval signatures section
```

**Markdown Template Structure (17 Sections):**

```markdown
# STEP 0: INDEPENDENT VERIFICATION REPORT

## 1. Title Banner
## 2. Customer Details Table
## 3. Executive Summary
## 4. Search 1: Adverse Media Check
## 5. Search 2: Directorships Check
## 6. Search 3: PEP Status Verification
## 7. Search 4: Professional Background
## 8. Search 5: Sanctions & Criminal Records
## 9. Step 0 Decision Gate Analysis
## 10. Material Misrepresentation Assessment
## 11. Risk Scoring Matrix
## 12. Risk Factor Details
## 13. Monitoring Requirements
## 14. Next Steps
## 15. Compliance Statement
## 16. Approvals
## 17. Regulatory References
```

### Method 2: fpdf2 (Python Fallback)

If `write_pdf` is unavailable or more precise layout control is needed, use Python's `fpdf2` library.

```python
from fpdf import FPDF

pdf = FPDF()
pdf.add_page()
pdf.set_font("Helvetica", "B", 20)
pdf.cell(0, 15, "STEP 0: INDEPENDENT VERIFICATION REPORT", ln=True, align="C")
pdf.set_font("Helvetica", "", 10)
pdf.cell(0, 8, f"Case ID: KYC-20260211-ONB-SMITH-001", ln=True, align="C")
pdf.cell(0, 8, f"Report Date: 11/02/2026", ln=True, align="C")
pdf.ln(10)

# Add sections...
pdf.set_font("Helvetica", "B", 14)
pdf.cell(0, 10, "CUSTOMER DETAILS", ln=True)
pdf.set_font("Helvetica", "", 10)
# ... populate with data ...

pdf.output("Step0_Report_JS_20260211.pdf")
```

**Note:** fpdf2 requires Python to be available in the environment. `write_pdf` does not have this dependency.

---

## Important Notes and Known Issues

### Consent Required for ALL MCP Tool Usage

Every MCP tool invocation must follow the HITL consent pattern. This is a non-negotiable compliance requirement:

- **Browser actions:** Ask before navigating, searching, or capturing screenshots.
- **File writes:** Ask before saving any file to the case folder.
- **Report generation:** Ask before generating Excel dashboards or PDF reports.
- **Folder creation:** Ask before creating case folder structures.

The analyst must explicitly confirm each action. Implied consent, batch consent, and auto-proceeding are not permitted.

---

### Always Use Absolute File Paths

All file operations via Desktop Commander must use absolute paths. Relative paths may resolve to unexpected locations.

```
CORRECT:
/Users/analyst/Documents/KYC_Cases/2026/02_February/Smith_John_20260211/Audit_Trail.txt

INCORRECT:
./KYC_Cases/2026/Smith_John/Audit_Trail.txt
../../Cases/Smith_John/Audit_Trail.txt
```

---

### Excel Content Must Be Valid JSON

When using `write_file` to create `.xlsx` files, the content parameter must be properly formed JSON. Common mistakes:

| Mistake | Result | Fix |
|---------|--------|-----|
| Unescaped quotes in cell values | JSON parse error | Escape with backslash: `\"` |
| Trailing commas in arrays | JSON parse error | Remove trailing commas |
| Single quotes instead of double | JSON parse error | Use double quotes only |
| Non-string/number cell values | Unexpected output | Convert all values to strings |

---

### BUG WARNING: Do NOT Put `===` in Any Excel Cell Value

**Known Bug in Desktop Commander:** If any cell value in the Excel JSON contains the string `===` (triple equals), Desktop Commander's serialiser converts the entire cell value to `[object Object]`.

```
BUG EXAMPLE:
  ["Risk Band", "LOW === 0-20"]
  --> Renders in Excel as: [object Object]

WORKAROUND:
  ["Risk Band", "LOW (0-20)"]
  ["Risk Band", "LOW -- Score range 0-20"]
  ["Risk Band", "LOW: 0 to 20"]
  --> All render correctly
```

**This applies to any cell in any sheet.** Always use parentheses, dashes, colons, or plain text instead of `===` in Excel cell values.

---

### Browser Automation Reliability

- **Always call `tabs_context_mcp` first** before any other Claude in Chrome tool. This initialises the tab group.
- **Create new tabs** for each search rather than reusing tabs from previous sessions.
- **Screenshots may fail** if the page has not fully loaded. Use `computer (action: wait, duration: 2)` before taking screenshots on slow-loading pages.
- **Form input** requires the element reference from `read_page` or `find`. If the reference is stale (page has changed), re-read the page.

---

### PDF Tools vs Desktop Commander

| Need | Use |
|------|-----|
| **Read** an existing PDF | PDF Tools (`read_pdf_content`) |
| **Create** a new PDF | Desktop Commander (`write_pdf`) |
| **Read PDF form fields** | PDF Tools (`read_pdf_fields`) |
| **Create** an Excel file | Desktop Commander (`write_file` with .xlsx) |

Do not confuse the two. PDF Tools is read-only for existing documents. Desktop Commander is the creation engine.

---

### Tool Availability Check

Before starting a workflow, verify that required MCP tools are available:

1. **Desktop Commander** -- Required for all workflows (file creation is mandatory).
2. **Claude in Chrome** -- Required for browser-based Step 0 searches. If unavailable, web search (built-in) can substitute for some searches, but evidence screenshots will not be captured.
3. **PDF Tools** -- Optional. Only needed if the customer has submitted PDF documents.
4. **Control Chrome** -- Optional. Supplementary tab management.

---

### Connector Placeholders

This plugin uses tool-agnostic `~~category` placeholders (see `CONNECTORS.md` for full details). MCP tools are the execution layer behind these placeholders:

| Placeholder | MCP Tool Used |
|-------------|--------------|
| `~~browser` | Claude in Chrome |
| `~~cloud storage` | Google Drive MCP, Box MCP (pre-configured in `.mcp.json`) |
| `~~CRM` | Connect via Cowork Settings |
| `~~email` | Connect via Cowork Settings |
| `~~chat` | Connect via Cowork Settings |

---

## Version History

| Version | Change |
|---------|--------|
| 2.3.0 | Unified MCP integration guide documenting all free tools |
| 2.2.0 | Added write_pdf support, Excel multi-sheet JSON format |
| 2.1.0 | Added Excel report generation via Desktop Commander |
| 2.0.0 | Added Claude in Chrome for Step 0 browser automation |
| 1.0.0 | Initial release with workflow templates |

---

**Version:** 2.3.0
**Author:** Vyayasan
**Repository:** https://github.com/vyayasan/kyc-analyst
