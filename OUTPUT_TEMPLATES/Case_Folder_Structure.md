# KYC Case Folder Structure - LOCKED SPECIFICATION

**CRITICAL: This folder structure is DETERMINISTIC and IDENTICAL for all analysts.**

---

## Root Directory Structure

```
KYC_Cases/
├── [YEAR]/
│   ├── [MM]_[MONTH_NAME]/
│   │   └── [LastName]_[FirstName]_[YYYYMMDD]/
│   └── [Next_Month]/
├── Dashboard.xlsx
├── Templates/
└── Archive/
```

---

## Per-Customer Folder (LOCKED STRUCTURE)

Every customer folder contains these 7 mandatory subfolders:

```
[CustomerFolder_YYYYMMDD]/
├── 00_Step0_Verification/
│   ├── Step0_Report.xlsx
│   ├── Step0_Report.md
│   ├── Step0_Report.pdf
│   ├── Audit_Trail.txt
│   ├── Evidence_Index.txt
│   ├── Screenshots/
│   │   ├── Adverse_Media_Search_[DATE].png
│   │   ├── Directorships_Search_[DATE].png
│   │   ├── PEP_Status_Search_[DATE].png
│   │   ├── Professional_Background_Search_[DATE].png
│   │   └── Sanctions_Search_[DATE].png
│   └── Evidence/
│       ├── News_Articles/
│       ├── Companies_House/
│       ├── PEP_Documents/
│       ├── Professional_Verification/
│       └── Sanctions_Evidence/
├── 01_Customer_Documents/
│   ├── ID_Documents/
│   ├── Proof_of_Address/
│   ├── Business_Documents/
│   ├── Source_of_Funds/
│   └── Additional_Documents/
├── 02_Risk_Assessment/
│   ├── Risk_Scoring_Matrix.xlsx
│   ├── Risk_Assessment_Report.docx
│   └── Risk_History/
├── 03_Screening_Results/
│   ├── PEP_Screening_[DATE].xlsx
│   ├── Sanctions_Screening_[DATE].xlsx
│   ├── Adverse_Media_Report_[DATE].xlsx
│   └── Escalations/
├── 04_Approvals/
│   ├── CDD_Approval_[DATE].docx
│   ├── Manager_Sign_Off_[DATE].pdf
│   ├── MLRO_Decision_[DATE].txt
│   └── Approval_History/
├── 05_Ongoing_Monitoring/
│   ├── Transaction_Monitoring.xlsx
│   ├── Periodic_Reviews/
│   ├── Transaction_Flags/
│   └── Investigation_Notes/
└── 06_Correspondence/
    ├── Initial_Contact_[DATE].docx
    ├── Information_Requests/
    └── Internal_Correspondence/
```

---

## File Naming Conventions (LOCKED)

**Reports:**
```
[ReportType]_[CustomerInitials]_[YYYYMMDD].xlsx
Example: Step0_Report_SJ_20260115.xlsx
```

**Screenshots:**
```
[SearchType]_Search_[YYYYMMDD].png
Example: Adverse_Media_Search_20260115.png
```

**Evidence:**
```
[EvidenceType]_[Source]_[YYYYMMDD].pdf
Example: News_Article_BBC_20260115.pdf
```

**Communications:**
```
[Type]_[Direction]_[YYYYMMDD].docx
Example: Information_Request_Outbound_20260115.docx
```

---

## 7 Mandatory Subfolders (LOCKED - Cannot deviate)

1. **00_Step0_Verification/** - Verification reports and all evidence
2. **01_Customer_Documents/** - ID, address, business documentation
3. **02_Risk_Assessment/** - Risk scoring matrix and assessment
4. **03_Screening_Results/** - PEP, sanctions, adverse media results
5. **04_Approvals/** - Manager and MLRO sign-offs
6. **05_Ongoing_Monitoring/** - Transaction monitoring and reviews
7. **06_Correspondence/** - All customer and internal communications

---

## File Organization Rules (LOCKED - Non-negotiable)

- Every case has all 7 subfolders (no exceptions)
- Folder names exact (no variations)
- File naming strictly standardized
- No custom folders permitted
- No spaces in file names (use underscores)
- Dates always YYYYMMDD format
- Archive for 5 years minimum

---

This folder structure is LOCKED and DETERMINISTIC.

**All analysts must follow this exact structure for every case.**

