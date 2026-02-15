# KYC Analyst - Connector Integration Guide

**Version:** 1.0.0
**Purpose:** Tool-agnostic connector integration using MCP (Model Context Protocol)

---

## How Connector Placeholders Work

This plugin uses **tool-agnostic placeholders** so workflows are not tied to any specific product. When you see `~~cloud storage` in a workflow, it means "use whatever cloud storage the user has connected" -- Google Drive, Box, OneDrive, SharePoint, or Dropbox.

### Placeholder Syntax: `~~category`

**Benefits:**
- Switch tools without rewriting workflows
- Use your organization's preferred tools
- One workflow works for all users
- No vendor lock-in

---

## Available Connectors

| Category | Placeholder | Pre-configured | Other Compatible Tools |
|----------|-------------|----------------|------------------------|
| **Cloud Storage** | `~~cloud storage` | Google Drive, Box | OneDrive, SharePoint, Dropbox |
| **Browser** | `~~browser` | Claude in Chrome | -- |
| **CRM** | `~~CRM` | -- | Salesforce, HubSpot, Dynamics 365 |
| **Project Management** | `~~project management` | -- | ServiceNow, Jira, Monday.com, Asana, Trello |
| **Email** | `~~email` | -- | Outlook, Gmail |
| **Communication** | `~~chat` | -- | Slack |
| **Document Management** | `~~document management` | -- | SharePoint, DocuWare, M-Files |
| **File System** | `~~filesystem` | Python os/io | -- |
| **PDF Generation** | `~~pdf` | fpdf2 (Python) | PDF Tools MCP |
| **Excel Generation** | `~~excel` | openpyxl (Python) | -- |

---

## MCP Tool Function Reference

### Claude in Chrome (~~browser)

Used for web research during Step 0 searches (Companies House, LinkedIn, news sites, sanctions databases).

**Core Functions:**
| Function | Purpose | Usage |
|----------|---------|-------|
| `tabs_context_mcp` | Get current tab context | Must call first before any browser action |
| `tabs_create_mcp` | Create new browser tab | Open new tab for research |
| `navigate` | Go to URL | Navigate to Companies House, LinkedIn, etc. |
| `read_page` | Get accessibility tree | Read page structure and elements |
| `get_page_text` | Extract page text | Get raw text from articles, profiles |
| `find` | Find elements by description | Locate search bars, buttons, links |
| `form_input` | Fill form fields | Enter search terms in Companies House |
| `computer` | Mouse/keyboard actions | Click, type, scroll, take screenshots |

**Workflow Integration Examples:**

```
# Search 2: Companies House Directorship Search
1. tabs_context_mcp -> get available tabs
2. navigate -> https://find-and-update.company-information.service.gov.uk/search/officers
3. find -> "search input field"
4. form_input -> enter customer name
5. computer -> click search button
6. get_page_text -> extract officer search results
7. Present findings to analyst for verification
```

```
# Search 4: LinkedIn Professional Verification
1. navigate -> https://www.linkedin.com/search/results/people/?keywords=[name]
2. get_page_text -> extract profile information
3. Compare declared role vs. found role
4. Document verification result
```

### File System Operations (~~filesystem)

Used for case folder creation, file management, and report storage.

**Methods:**
- Python `os.makedirs()` for folder creation
- Python file I/O for text files

**Workflow Integration:**
```
# Case Folder Creation (Stagegate 3)
Create directory structure:
  KYC-[DATE]-ONB-[NAME]-[SEQ]/
    001_CASE_METADATA/
    002_STEP_0_SEARCHES/
    003_VERIFICATION_OUTCOMES/
    004_DECISION_DOCUMENTATION/
    005_ESCALATION_BRIEF/
    006_AUDIT_TRAIL/
```

### PDF Generation (~~pdf)

Used for creating professional 17-section PDF reports.

**Methods (in priority order):**
1. **fpdf2 (Python)** - Preferred for full formatting control
2. **PDF Tools MCP** - For reading/analyzing existing PDFs

**Compatibility note:** Use ASCII alternatives (`[OK]`, `[X]`, `[->]`) instead of Unicode characters with the default Helvetica font.

### Excel Generation (~~excel)

Used for creating 4-sheet professional Excel dashboards.

**Method:** openpyxl (Python)

**Compatibility note:** Avoid `===` in cell values when writing via MCP file tools — use parentheses or dashes instead.

**4-Sheet Structure:**
- Sheet 1: Executive Summary (customer profile, all search results, decision)
- Sheet 2: Directorships (all companies with disclosure status)
- Sheet 3: Discrepancies (declared vs actual comparison)
- Sheet 4: Risk Assessment (four-factor scoring with weighted totals)

---

## HITL Consent Patterns for MCP Tools

All MCP tool actions require analyst consent at stagegate checkpoints.

### Pattern 1: Browser Search Consent
```
========================================
SEARCH [N]: [SEARCH NAME]
========================================

I will search [SOURCE] for [CUSTOMER NAME].

Sources: [List of databases]

========================================
ANALYST CONSENT REQUIRED
========================================

Type 'proceed' to authorize browser automation
Type 'manual' to enter findings yourself
```

### Pattern 2: File Operation Consent
```
========================================
CASE FOLDER CREATION
========================================

I will create the case folder structure at:
[PATH]

Subfolders: 001-006 per locked specification

========================================
Type 'create-folder' to proceed
```

### Pattern 3: Report Generation Consent
```
========================================
[EXCEL/PDF] REPORT GENERATION
========================================

I will generate the [report type].

========================================
ANALYST APPROVAL REQUIRED
========================================

Type 'generate-excel' or 'generate-pdf' to proceed
```

---

## How to Use Connectors in Workflows

### Cloud Storage (Saving Case Files)
```
Save all outputs to ~~cloud storage under KYC/Cases/2026/
```
Works with: Google Drive, Box, OneDrive, SharePoint, Dropbox

### CRM (Customer Records)
```
Retrieve customer profile from ~~CRM for [Customer Name]
Update ~~CRM with completed KYC status and risk rating
```
Works with: Salesforce, HubSpot, Dynamics 365

### Browser (Web Research)
```
Use ~~browser to search Companies House for [Company Name]
Use ~~browser to verify LinkedIn profile for [Person Name]
```
Works with: Claude in Chrome

### Email (Notifications & Escalations)
```
Send escalation brief to Manager via ~~email
Notify customer of additional documentation required via ~~email
```
Works with: Outlook, Gmail

### Communication (Team Alerts)
```
Alert compliance team via ~~chat about HIGH risk case
Post daily screening summary to ~~chat compliance channel
```
Works with: Slack

---

## Pre-Configured MCP Servers

The `.mcp.json` file pre-configures:
- **Google Drive** - For case file storage
- **Box** - For enterprise document management

Additional MCP servers detected at runtime:
- **Claude in Chrome** - Browser automation (auto-detected)
- **PDF Tools** - PDF analysis and generation (auto-detected)

To add other connectors, update `.mcp.json` with the appropriate MCP server URL.

---

## Setup Instructions

### Step 1: Connect Tools in Cowork
1. Open Cowork Settings
2. Navigate to Connectors / MCP Servers
3. Connect your preferred tools for each category

### Step 2: Verify Connection
Test with a simple command:
```
List files in ~~cloud storage under KYC/
```

### Step 3: Use in Workflows
All workflow templates in WORKFLOW_TEMPLATES.md already include connector placeholders. The onboard.md command integrates MCP tools at each stagegate.

---

**Version:** 1.0.0
**Author:** Vyayasan
