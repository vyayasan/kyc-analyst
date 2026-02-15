# KYC Analyst v2.3.0 - Quick Start Guide

**Complete your first KYC case in 10 minutes**

---

## Before You Start

✅ Have ready:
- Customer ID (passport, national ID, or driver's license photo)
- Proof of address (utility bill or bank statement <3 months)
- Customer application form with declared information

Connected (optional but recommended):
- ~~cloud storage (Google Drive, Box, etc.)
- ~~browser (Claude in Chrome) -- for automated web research
- ~~CRM (Salesforce, HubSpot, etc.)
- Python 3 with openpyxl and fpdf2 -- for Excel/PDF report generation

**Important:** The onboarding workflow follows 17 mandatory stagegates. Each gate requires your explicit consent (e.g., 'proceed', 'confirm', 'generate-excel'). See `commands/onboard.md` for the full specification.

---

## Your First Case: Basic Individual

### Step 1: Open Workflow Templates (1 minute)

Navigate to: `WORKFLOW_TEMPLATES.md`

Find: **Template 1: Individual Client - Standard Employment**

---

### Step 2: Copy and Customize (2 minutes)

Copy the template and fill in real information:

```
Execute KYC onboarding with Step 0 verification for individual client.

CLIENT DETAILS:
- Full Name: Sarah Johnson
- Date of Birth: 15/03/1985
- Nationality: British
- Country of Residence: United Kingdom
- Occupation: Software Engineer
- Employer: Tech Solutions Ltd
- Expected Activity: Salary deposits, personal expenses

DOCUMENTS PROVIDED:
- [✓] Valid passport
- [✓] Utility bill dated 15/01/2026
- [✓] Employment contract
- [✓] Application form

[Rest of template as-is - don't modify Step 0 instructions]
```

---

### Step 3: Execute in Claude (5 minutes)

Paste the filled template into Claude and press Enter.

**What happens automatically:**
1. ✅ Claude searches 72+ adverse media sources
2. ✅ Claude checks Companies House for directorships
3. ✅ Claude screens 5 PEP databases
4. ✅ Claude verifies LinkedIn and professional background
5. ✅ Claude screens 12 sanctions/legal lists
6. ✅ Claude calculates heuristic risk score
7. ✅ Claude generates 4-sheet Excel dashboard
8. ✅ Claude generates 17-section PDF report

---

### Step 4: Review Decision Gate (2 minutes)

Claude will present decision:

**If PROCEED:**
```
STEP 0 DECISION: PROCEED

All searches: CLEAR
- Adverse Media: No findings
- Directorships: None found
- PEP Status: Not a PEP
- Professional Background: Verified via LinkedIn
- Sanctions: Clear

Risk Score: 18 (LOW)
Recommendation: Proceed to standard CDD
```

✅ **Action:** Continue with customer onboarding

**If ESCALATE:**
```
STEP 0 DECISION: ESCALATE

Issue identified: Undisclosed directorship found
- Declared: No business interests
- Actual: Director of ABC Consulting Ltd since 2022
- Assessment: Material non-disclosure

Risk Score: 72 (HIGH)
Recommendation: Escalate to Manager + MLRO
```

⚠️ **Action:** Send escalation brief to management

---

### Step 5: Save Outputs (Optional - 1 minute)

If you have connectors setup:

```
Save all outputs to ~~cloud storage under KYC/Cases/2026/Individual/

Update ~~CRM for Sarah Johnson:
- KYC Status: Complete
- Risk Rating: LOW
- Case Reference: KYC-20260211-ONB-JOHNSON-001
```

---

## What You Get

### 4-Sheet Excel Dashboard
- **Sheet 1:** Executive Summary
  - Customer profile
  - All 5 search results
  - Decision (PROCEED/ESCALATE)
  
- **Sheet 2:** Directorships
  - All companies (if any)
  - Disclosure status
  
- **Sheet 3:** Discrepancies
  - Declared vs Actual comparison
  
- **Sheet 4:** Risk Assessment
  - Geographic Risk (30%)
  - Customer Risk (35%)
  - Product Risk (25%)
  - Channel Risk (10%)
  - **Overall Score:** LOW/MEDIUM/HIGH/CRITICAL

### 17-Section PDF Report
Professional client-ready report with:
- Executive summary
- Complete verification evidence
- Risk assessment
- Regulatory compliance statements
- Signed analyst certification

### Case Folder
```
KYC-20260211-ONB-JOHNSON-001/
├── 001_CASE_METADATA/
│   └── CASE_METADATA.md
├── 002_STEP_0_SEARCHES/
│   ├── Search_1_Findings.md
│   ├── Search_2_Findings.md
│   ├── Search_3_Findings.md
│   ├── Search_4_Findings.md
│   ├── Search_5_Findings.md
│   └── STEP_0_VERIFICATION_REPORT.md
├── 003_VERIFICATION_OUTCOMES/
├── 004_DECISION_DOCUMENTATION/
├── 005_ESCALATION_BRIEF/ (if needed)
└── 006_AUDIT_TRAIL/
    └── AUDIT_TRAIL.md (immutable)
```

---

## Next Steps

### For More Complex Cases

**HNWI/High Net Worth:**
→ Use Template 2 in WORKFLOW_TEMPLATES.md

**Corporate/SME:**
→ Use Template 3 in WORKFLOW_TEMPLATES.md

**Complex Corporate Structure:**
→ Use Template 4 in WORKFLOW_TEMPLATES.md

**Existing Customer Refresh:**
→ Use Template 5 in WORKFLOW_TEMPLATES.md

---

### Setup Connectors (Recommended)

**Why:** Automates saving, CRM updates, notifications

**How:** See CONNECTORS.md for setup instructions

**Time:** 10-15 minutes one-time setup

**Benefit:** Saves 5-10 minutes per case going forward

---

## Common Questions

### Q: How long does a basic case take?
**A:** 10-15 minutes from start to completed reports

### Q: Do I need to connect cloud storage?
**A:** No, but recommended. Without it, you'll copy-paste outputs manually.

### Q: What if Step 0 finds something?
**A:** Claude provides escalation brief automatically. Send to Manager + MLRO.

### Q: Can I customize the searches?
**A:** Step 0 searches are mandatory per v2.2.0. Additional searches can be added after.

### Q: What if customer has no LinkedIn?
**A:** Document as "No LinkedIn presence found" and use alternative verification (company website, trade publications).

### Q: How do I handle PEPs?
**A:** Automatic escalation for EDD. Senior management approval required before onboarding.

---

## Troubleshooting

### "Cannot find customer on Companies House"
✅ **Normal:** Many individuals have no directorships
✅ **Document:** "No directorships found"
✅ **Proceed:** If all other searches clear

### "Sanctions screening shows possible match"
⚠️ **Stop:** Assess false positive
⚠️ **Compare:** Name, DOB, location similarities
⚠️ **Decision:** True match = reject; False positive = document and proceed
⚠️ **Escalate:** If uncertain

### "Risk score is HIGH but customer seems low risk"
ℹ️ **Check:** Which factors drove score up?
ℹ️ **Common:** High-risk geography or industry
ℹ️ **Action:** Review factor weights, may need EDD even if customer "seems" low risk

---

## Tips for Fast Processing

### ✅ Do:
- Prepare all documents before starting
- Use template as-is for first case (learn the flow)
- Read decision gate carefully
- Save case folder for audit trail

### ❌ Don't:
- Skip Step 0 searches (mandatory)
- Proceed with unresolved discrepancies
- Modify locked template formats
- Delete audit trail files

---

## Need Help?

📖 **Full Documentation:** See skills/onboarding/SKILL.md
📋 **All Templates:** See WORKFLOW_TEMPLATES.md
🔌 **Connector Setup:** See CONNECTORS.md
📊 **Output Examples:** See EXAMPLES/ folder (coming soon)

**Support:** contact@vyayasan.com
**GitHub:** https://github.com/vyayasan/kyc-analyst

---

**That's it! You've completed your first KYC case.** 🎉

For your next case, it'll be even faster (5-10 minutes) as you're now familiar with the flow.

---

**Version:** 2.3.0
**Author:** Vyayasan
**Last Updated:** February 2026
