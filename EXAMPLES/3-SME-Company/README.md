# Case 3: SME-Company
## Corporate Onboarding with UBO Verification

**Case ID:** KYC-20260211-ONB-TECHVENTURES-001
**Customer:** TechVentures Limited (Anonymized)
**Scenario:** UK SME with clear beneficial ownership structure
**Risk Level:** MEDIUM (Low-Medium)
**Decision:** PROCEED

---

## What This Example Demonstrates

This example shows **corporate/SME onboarding** where beneficial ownership verification is central to the process. Unlike individual cases, corporate onboarding requires penetrating ownership layers to identify all natural persons with >25% beneficial ownership per AMLD5 requirements.

### Key Characteristics
- Legal entity (company) rather than individual
- Clear, transparent ownership structure (2 main shareholders, 35% each)
- Verified UBOs (beneficial owners) at natural person level
- Straightforward business (software/IT services)
- Profitable, stable financial position
- No hidden or complex ownership chains

### Learning Objectives
Students should use this example to understand:
1. How corporate KYC differs from individual KYC
2. Beneficial ownership identification (AMLD5 requirement)
3. UBO screening process (directors + beneficial owners)
4. How to penetrate ownership structures to natural persons
5. Corporate verification techniques
6. Financial statement review for corporate KYC
7. When corporate cases can be analyst-approved vs escalated

---

## Corporate KYC vs Individual KYC

### Individual KYC (Case 1: John Smith)
- One person to verify
- Identity document + address + employment
- Personal background checks
- Simple decision: PROCEED or ESCALATE

### Corporate KYC (Case 3: TechVentures)
- Multiple individuals to verify (directors + UBOs)
- Company registration + Articles + Financial accounts
- Ownership structure analysis
- Beneficial owner identification (>25% threshold)
- Individual screening for directors AND beneficial owners
- More complex decision logic

### Key Difference: Beneficial Ownership

For corporate clients, you must:
1. **Identify all natural persons with >25% ownership** (UBOs)
2. **Screen EACH UBO** as if they were direct customers
3. **Penetrate ownership structures** (trace through entities to natural persons)
4. **Verify beneficial ownership** is properly documented
5. **Flag any concealment** of beneficial ownership

---

## UBO Identification (AMLD5 Requirement)

### What is AMLD5?

**AMLD5** = EU Anti-Money Laundering Directive 5
- Implemented in UK as **UK Money Laundering Regulations 2017 (as amended)**
- Requires identification of all "beneficial owners"
- Beneficial Owner = Natural person with >25% ownership or control

### The 25% Threshold

Why 25%?
- Below 25% = Minority interest (lower risk)
- 25%+ = Significant control (higher risk, requires verification)
- This is the regulatory standard for "beneficial owner"

### TechVentures Beneficial Ownership Analysis

**Shareholding Structure:**
```
TechVentures Limited (100%)
├── Sarah Johnson: 35% → EXCEEDS 25% → UBO
├── Michael Chen: 35% → EXCEEDS 25% → UBO
└── Investment Partner Limited: 20% → Below 25% → Not UBO
    └── Must still check if any natural person owns >25% of Investment Partner
        └── Holds 10 employees, each <5% → No natural person >25%
```

**Result:** 2 qualifying UBOs (Sarah Johnson and Michael Chen)

### UBO Screening in This Case

**Sarah Johnson - UBO 1:**
- Shareholding: 35% (qualifying)
- Role: CEO & Director
- Screening: All 5 Step 0 searches executed
- Result: CLEAR - No adverse findings

**Michael Chen - UBO 2:**
- Shareholding: 35% (qualifying)
- Role: CTO & Director
- Screening: All 5 Step 0 searches executed
- Result: CLEAR - No adverse findings

**Investment Partner Limited - Non-UBO:**
- Shareholding: 20% (non-qualifying)
- Structure: Employee investment scheme
- Underlying owners: 10 employees, each <5%
- Result: No natural person exceeds 25% threshold; no concealment detected

---

## Corporate Verification Techniques

### 1. Companies House Officer Search
**Purpose:** Identify all directors and their holdings

**For TechVentures:**
- Directors: Sarah Johnson (CEO), Michael Chen (CTO)
- No disqualifications found
- Both appointed at incorporation (15/03/2015)
- Both active, no removals

### 2. Shareholding Analysis
**Purpose:** Map complete ownership structure

**For TechVentures:**
- Sarah Johnson: 35% (direct shareholding)
- Michael Chen: 35% (direct shareholding)
- Investment Partner Limited: 20% (entity shareholding)
- Total: 100% accounted for
- No nominee arrangements detected
- No trust structures concealing ownership

### 3. Financial Statement Review
**Purpose:** Verify company is legitimate operating business

**For TechVentures (2025 Accounts):**
- Revenue: £1,050,000
- Profit: £145,000
- Assets: £420,000
- 11 consecutive years profitable
- Assessment: Legitimate, stable business

### 4. Business Activity Verification
**Purpose:** Confirm company does what it claims

**For TechVentures:**
- Website: www.techventures.uk (active)
- Client list: 30+ corporate clients visible
- Industry: Software development & IT consulting
- Business model: B2B services
- Assessment: Legitimate software company

### 5. Director Background Verification
**Purpose:** Screen directors as individuals

**For TechVentures:**
- Sarah Johnson: 20+ years IT industry, professional progression verified
- Michael Chen: 18+ years technical background, expertise verified
- Both: Clean records, no adverse findings, no PEP status

---

## Risk Assessment for SME

### SME Risk Factors

Why is TechVentures rated MEDIUM (not LOW)?

| Factor | Reason |
|--------|--------|
| Industry | Tech/software = moderate risk (not high-risk sector like MSB or crypto) |
| Scale | £1m revenue = SME size (lower risk than enterprise) |
| Profitability | 11 years profitable = established (low risk) |
| Ownership | Clear, transparent (low risk) |
| Geography | UK-based (low-risk jurisdiction) |
| Directors | Both directors: clean records, professional (low risk) |
| **Overall** | **Multiple low-risk factors = MEDIUM-LOW rating** |

Risk Score: 17/100 = MEDIUM band (0-20 range)

Note: This is MEDIUM only because it's in the moderate range. Compared to:
- Case 1 (John Smith): 13/100 = LOW
- Case 3 (TechVentures): 17/100 = MEDIUM (but low end)
- Case 2 (Alexander Thompson): 62/100 = HIGH

TechVentures is straightforward SME with minimal risk.

---

## Files Included

### 1. INPUT-Customer-Details.md
Complete corporate application with company details, beneficial ownership structure, directors information, and financial overview.

### 2. EXPECTED-Excel-Dashboard.txt
5-sheet corporate dashboard:
- Company Profile & Verification
- Ownership Structure & Beneficial Ownership
- Director & UBO Screening Results
- Corporate Risk Assessment
- Decision & Approval

### 3. EXPECTED-PDF-Report.md
Professional corporate KYC report with detailed beneficial ownership analysis, director verification, business profile, and regulatory compliance assessment.

### 4. EXPECTED-Audit-Trail.txt
14-event immutable audit trail from application through approval.

### 5. README.md (This File)
Complete training documentation for corporate KYC workflows.

---

## Key Learning Points

### 1. UBO Identification is Mandatory
AMLD5 requires identification of all natural persons with >25% ownership. This is not optional—it must be done for every corporate customer.

### 2. Transparent Ownership Simplifies Process
When shareholding is straightforward (2 owners at 35% each), the process is simple:
1. Identify qualifying UBOs (those >25%)
2. Screen each UBO
3. Confirm no hidden structures
4. Done

Complex ownership (multiple layers, trusts, nominee arrangements) requires deeper penetration analysis.

### 3. Directors ≠ Always UBOs
A person can be a director without being a UBO:
- Director: Person appointed to manage company
- UBO: Person with >25% beneficial ownership

In TechVentures, Sarah Johnson and Michael Chen are BOTH directors AND UBOs (35% each).
In Investment Partner Limited, employees are UBOs through their shareholding, but may not be directors of TechVentures.

### 4. Entities Must Be Penetrated
When a company (like Investment Partner Limited) is a shareholder, you must:
1. Identify who owns/controls that entity
2. Check if any natural person behind it exceeds 25%
3. If yes, they are an indirect UBO and must be screened

In TechVentures' case: Investment Partner Limited is 20% shareholder, but no individual owns >25% of it, so no further penetration needed.

### 5. Analyst Approval is Appropriate for MEDIUM Risk
Unlike HNWI cases (HIGH risk, requiring manager approval), this MEDIUM-risk SME case can be approved by analyst. The risk is transparent and manageable with standard monitoring.

---

## Common Questions

**Q: Why do we screen both the directors and UBOs separately?**
A: Regulatory requirement. Directors manage the company; UBOs own the company. Both must be verified. They're often the same people, but screening is done separately to ensure complete coverage.

**Q: What if we can't identify all UBOs?**
A: Then you cannot proceed. AMLD5 explicitly requires beneficial owner identification. Unable to identify = Unable to meet regulatory requirement = Cannot onboard.

**Q: What makes this MEDIUM risk and not LOW?**
A: Industry and product risk push it slightly higher. A salaried employee (Case 1, 13/100) has very simple, verifiable income. A business with multiple revenue streams (Case 3, 17/100) has slightly more complexity. Still low-risk, but in the MEDIUM range.

**Q: Could this company escalate to manager for EDD?**
A: Only if something changed. If the risk assessment had revealed issues (PEP status, adverse findings, high-risk ownership structure), it would escalate. But with clean verification and transparent ownership, analyst approval is appropriate.

**Q: How often is this company reviewed?**
A: Annual (12 months). Next review would be 11 February 2027. At that point:
- Confirm registered office unchanged
- Review latest financial accounts
- Confirm directors/UBOs unchanged
- Re-screen for adverse findings
- Assess if company profile has changed

---

## Regulatory Basis

**AMLD5 (EU Directive 5/2018)**
- Article 3: Definition of beneficial owner
- Article 13: Customer due diligence obligations
- Article 14: Enhanced due diligence
- Article 30: Beneficial owner registration

**UK Money Laundering Regulations 2017 (as amended)**
- Regulation 10: Customer due diligence requirements
- Regulation 11: Verification on basis of documents
- Schedule 1 & 2: Beneficial owner identification guidance

**FCA HANDBOOK**
- SYSC 6: Systems and Controls
- COND 2.3R: Customer due diligence

---

## Conclusion

This example demonstrates professional, compliant SME onboarding with particular focus on beneficial ownership identification per AMLD5. The process shows:
- **Identification:** How to map ownership structures
- **Penetration:** How to reach natural persons behind entities
- **Verification:** How to screen directors and UBOs
- **Assessment:** How to evaluate corporate risk
- **Approval:** When analyst approval is appropriate for MEDIUM-risk cases

The key takeaway: Corporate KYC is more complex than individual KYC due to ownership structure analysis, but straightforward companies with clear ownership can be processed efficiently by analysts without escalation.

---

**Example Version:** 1.0
**Version Date:** 11 February 2026
**Applicable To:** KYC Analyst v1.0.0
**Status:** Ready for Training & Testing
