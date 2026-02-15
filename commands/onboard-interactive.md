---
description: Interactive customer onboarding with Step 0 independent verification (dialog-based, 17 stagegates)
argument-hint: "<customer name>"
---

# Onboard (Interactive Mode)

> If you see unfamiliar placeholders or need to check which tools are connected, see [CONNECTORS.md](../CONNECTORS.md).

Interactive customer onboarding with guided conversation for comprehensive KYC/AML compliance including mandatory Step 0 independent verification with five independent searches. This mode follows the same **17 mandatory stagegates** as the standard onboard command but uses a conversational Q&A approach.

## Usage

```
/kyc:onboard-interactive <customer name>
```

## How Interactive Mode Works

Interactive mode uses the same 17-stagegate workflow as `/kyc:onboard` but presents each gate as a conversational prompt rather than a batch template. Every stagegate requires explicit analyst consent before proceeding.

### Phase 1: Customer Information (Stagegates 1-5)

**Stagegate 1 - Case Initialization:**
Claude confirms case details and asks:
- "What type of customer is this? Individual, Corporate, or Trust?"
- "What country/jurisdiction?"

**Stagegate 2 - Information Gathering:**
Claude asks questions to collect:
- Customer type (Individual/Corporate/Trust)
- Basic identification details (name, DOB, nationality)
- Business/employment information
- Documents available
- Source of funds/wealth

**Stagegate 3 - Case Folder Creation:**
Claude creates the case folder and asks for confirmation:
- "I've created case folder KYC-[DATE]-ONB-[NAME]-[SEQ]. Ready to proceed?"

**Stagegate 4 - Customer Details Entry:**
Claude populates CASE_METADATA.md and asks:
- "Please confirm these details are correct: [summary]. Type 'confirm' to proceed."

**Stagegate 5 - Step 0 Commencement:**
- "All information gathered. Ready to begin Step 0 independent verification? Type 'begin-step-0' to start."

### Phase 2: Step 0 Verification (Stagegates 6-12)

Each search follows the consent-execute-verify cycle:

**Stagegate 6 - Search 1: Adverse Media**
- "I'll search 72+ adverse media sources for [name]. Type 'proceed' to authorize."
- Claude executes search, presents findings
- "Here's what I found: [results]. Type 'confirm' to accept and continue."

**Stagegate 7 - Search 1.5: ICIJ Offshore Leaks**
- "I'll check the ICIJ Offshore Leaks Database (Panama Papers, Paradise Papers, Pandora Papers). Type 'proceed' or 'skip' if low-risk."

**Stagegate 8 - Search 2: Directorships**
- "I'll search Companies House for all directorships. Type 'proceed' to authorize."
- Claude presents all found companies with disclosure status
- "I found [X] directorships. [Y] were declared, [Z] were NOT declared. Type 'confirm'."

**Stagegate 9 - Search 3: PEP Status**
- "I'll check 5 PEP databases. Type 'proceed' to authorize."

**Stagegate 10 - Search 4: Professional Background**
- "I'll verify employment at [employer] via LinkedIn and company sources. Type 'proceed'."

**Stagegate 11 - Search 5: Sanctions/Crime**
- "I'll screen against 12 sanctions and legal databases. Type 'proceed'."

**Stagegate 12 - Data Verification**
- After each search, Claude presents extracted data and waits for analyst to type 'confirm'

### Phase 3: Decision Gate (Stagegates 13-14)

**Stagegate 13 - Report Compilation & Decision:**
- "All 5 searches complete. Type 'compile-report' to generate the Step 0 Verification Report."
- Claude compiles report, calculates risk score, presents decision gate
- "Risk Score: [X]/100 ([BAND]). Decision: [PROCEED/ESCALATE]. Type 'approve-decision' to confirm."

**Stagegate 14 - Escalation (Conditional):**
- If ESCALATE: "I'll prepare the escalation brief. Type 'prepare-escalation'."
- If PROCEED: Automatically moves to Stagegate 15

### Phase 4: Output Generation (Stagegates 15-17)

**Stagegate 15 - Excel Report:**
- "Ready to generate the 4-sheet Excel dashboard? Type 'generate-excel'."

**Stagegate 16 - PDF Report:**
- "Ready to generate the 17-section PDF report? Type 'generate-pdf' or 'skip-pdf'."

**Stagegate 17 - Case Finalization:**
- Claude runs QA checklist and presents final summary
- "Case complete. All deliverables generated. Audit trail locked."

## Key Differences from Standard Mode

| Feature | Standard (/kyc:onboard) | Interactive (/kyc:onboard-interactive) |
|---------|------------------------|---------------------------------------|
| Information input | Provided in command | Gathered via Q&A dialog |
| Stagegate presentation | Formatted blocks | Conversational prompts |
| Consent commands | Same keywords | Same keywords |
| Searches | Same 5+1 searches | Same 5+1 searches |
| Outputs | Same reports | Same reports |
| Stagegate enforcement | 17 mandatory gates | 17 mandatory gates |

## Features

- Conversational guidance through all 17 stagegates
- Same HITL consent requirements as standard mode
- Real-time search result processing with ~~browser
- Immediate discrepancy identification
- Case folder auto-creation via ~~filesystem
- Excel dashboard via openpyxl (~~excel)
- PDF report via fpdf2 (~~pdf)
- Escalation routing with explanations
- Immutable audit trail

---

**Version:** 2.3.0
**Author:** Vyayasan
