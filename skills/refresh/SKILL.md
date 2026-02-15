---
name: refresh
description: >
  Periodic customer refresh with re-verification of original due diligence to detect material changes
  and maintain compliance with ongoing due diligence requirements. Triggers include time-based review
  (annual HIGH risk, 2-3 year intervals for MEDIUM/LOW), risk-based escalation (score changes, business
  pivots), and event-based alerts (sanctions, adverse media, regulatory actions).
user-invocable: true
category: compliance
estimated-duration: 45 minutes
---

# Customer Refresh Skill - v1.0.0

Periodic customer review with independent re-verification to maintain ongoing due diligence compliance and detect material changes.

## Overview

Refresh is mandatory continuing monitoring required under AMLD5 (UK/EU), FinCEN CDD Rule (US), and MENA regional regulations. This skill re-runs the Step 0 onboarding verification framework to establish whether material changes have occurred and risk profile remains appropriate.

**Key Principle:** Refresh detects what *changed*, not what was previously found.

## Why Refresh Matters

Regulatory frameworks across all jurisdictions mandate ongoing monitoring because:

1. **Risk Emergence:** Beneficial ownership, regulatory status, and threat profiles evolve. A low-risk business can pivot to high-risk sectors; transparent ownership can become hidden.

2. **Sanction Exposure:** Designation lists update monthly. Customers or their beneficial owners may become PEPs, fall under sanctions, or face criminal charges.

3. **Adverse Media Detection:** News of regulatory enforcement, criminal convictions, or corruption allegations may not appear during onboarding but emerge later.

4. **Beneficial Ownership Verification:** AMLD5 and FinCEN BOI Rule require periodic confirmation that beneficial ownership information remains accurate and complete.

## Refresh Intervals by Risk Category

See detailed regulatory requirements:
- **UK/EU:** [regulations-uk-eu.md](references/regulations-uk-eu.md)
- **MENA:** [regulations-mena.md](references/regulations-mena.md)
- **US:** [regulations-us.md](references/regulations-us.md)

**Quick Reference:**
- HIGH: Annual (all regions)
- MEDIUM: 24 months (UK/EU), 6 months (MENA)
- LOW: 36 months (UK/EU), 12 months (MENA/US)

## Refresh Triggers

See complete trigger library: [refresh-triggers.md](references/refresh-triggers.md)

**Types of Triggers:**
- **Time-based:** Scheduled per risk category
- **Risk-based:** Customer risk score change, business model shift, regulatory classification change
- **Event-based:** Sanctions alert, adverse media, regulatory enforcement, MLRO escalation closure

## Step-by-Step Refresh Procedure

### Step 1: Initiate Refresh [HITL Checkpoint]

**Analyst Actions:**
1. Open customer profile and verify last refresh date vs. risk category
2. Confirm trigger: Time-based, risk-based, or event-based (document in case file)
3. Export original onboarding report to compare findings
4. Review original 5 searches performed at Step 0 onboarding:
   - Search 1: Google/LinkedIn/Business Registry (public profile, business interests)
   - Search 2: Sanctions/Regulatory (OFAC/PEP databases, regulatory records)
   - Search 3: Adverse Media (news, adverse events, regulatory actions)
   - Search 4: Corporate Records (ownership structure, filings, director changes)
   - Search 5: Financial Risk (credit reports, industry risk indicators, market data)

**Manager Checkpoint:**
- [ ] Confirm refresh is timely (not premature, not overdue)
- [ ] Verify trigger is documented and justified
- [ ] Approve proceeding to Step 2

---

### Step 2: Re-Run 5 Independent Searches [HITL Checkpoint]

Repeat exact searches from onboarding to establish fresh baseline.

**Search 1: Public Profile & Business Interests**
- Google search: Customer name + company name
- LinkedIn profile review
- Company registry filings (Companies House UK, SEC Edgar US, local registries)
- Business database review (Bloomberg, Crunchbase, business.gov.uk)
- **Compare to original:** New directorships? Business pivots? Changed sectors?

**Search 2: Sanctions & Regulatory Databases**
- OFAC SDN List (US)
- EU Sanctions Lists
- UK Office of Financial Sanctions Implementation (OFSI)
- UN Consolidated Sanctions List
- INTERPOL Red/Yellow Notices
- **Compare to original:** Any new matches? Designations on family members?

**Search 3: Adverse Media Review**
- Google News search (5-year lookback)
- Reuters/Bloomberg news terminals
- Adverse media monitoring service (LexisNexis, World-Check, Refinitiv)
- Regulatory enforcement databases
- Criminal record databases (jurisdiction-specific)
- **Compare to original:** New media coverage? Regulatory actions? Criminal charges?

**Search 4: Corporate Structure & Beneficial Ownership**
- Company registry beneficial ownership filings
- Corporate structure diagrams (if available from data providers)
- Director and shareholder searches
- Related entity searches (common shareholders, directors)
- Ownership chain verification
- **Compare to original:** New beneficial owners? Changes in shareholder structure? Hidden beneficial ownership patterns?

**Search 5: Financial Risk Indicators**
- Credit report review (if available and permitted)
- Financial viability indicators (industry reports, market data)
- Industry risk assessment (sector risk changes?)
- Geographic risk mapping (new operations in high-risk jurisdictions?)
- Transaction pattern baseline (if monitoring data available)

**Analyst Documentation:**
- Record all 5 searches with dates, platforms used, search terms
- Screenshot or document key findings
- Note "No new findings" vs. "New findings" for each search

**Manager Checkpoint:**
- [ ] Confirm all 5 searches were completed
- [ ] Verify search methodology matches original onboarding
- [ ] Approve moving to Step 3 (change comparison)

---

### Step 3: Identify Material Changes [HITL Checkpoint]

Compare refresh findings to original onboarding findings.

**Material Changes (Automatic Escalation):**

1. **Beneficial Ownership Changes**
   - New beneficial owner with 25%+ stake
   - Beneficial owner departure (25%+ stakeholder)
   - Evidence of beneficial ownership concealment
   - Change to nominee or trust ownership structure
   - **Action:** ESCALATE to Manager + MLRO

2. **Business Structure Changes**
   - Corporate restructuring (merger, acquisition, restructure)
   - Business sector pivot to high-risk sector (crypto, gambling, trade finance, weapons)
   - Loss of regulatory status or license
   - **Action:** ESCALATE to Manager + MLRO

3. **Regulatory Changes**
   - Customer becomes regulated entity (escalate for new due diligence)
   - Customer loses regulatory authorization
   - Regulatory enforcement action against customer or principals
   - **Action:** ESCALATE to Manager + MLRO

4. **Sanctions & Adverse Media Changes**
   - Sanctions designation (any customer or beneficial owner)
   - Adverse media: regulatory enforcement, criminal conviction, corruption allegation
   - INTERPOL or criminal investigation listing
   - **Action:** IMMEDIATE ESCALATION (same-day MLRO notification)

**Non-Material Changes (Risk Assessment Update):**
- Address change within expected geographic scope
- Standard corporate governance changes (board rotation, officer changes)
- Business expansion within same risk sector
- Beneficial ownership updates confirming prior findings

**Analyst Documentation:**
- List all findings (new and unchanged)
- Flag each finding as "Material Change" or "Update"
- For material changes: document source, date discovered, risk implication
- For updates: brief note confirming prior findings still valid

**Manager Checkpoint:**
- [ ] Confirm change classifications (material vs. non-material)
- [ ] Verify material changes are documented with source evidence
- [ ] Determine escalation path (Manager review, MLRO notification, immediate quarantine)

---

### Step 4: Risk Re-Assessment [HITL Checkpoint]

Update customer risk category based on refresh findings.

**Risk Categories:**
- **HIGH:** PEPs, beneficial owners of complex structures, high-value customers, high-risk sectors, frequent transactions to high-risk jurisdictions, family of sanctions targets
- **MEDIUM:** Established businesses in moderate-risk sectors, some international activity, standard corporate governance
- **LOW:** EU regulated entities, transparent ownership, narrow scope of business, domestic focus, established markets

**Reassessment Decision Tree:**
1. Were any MATERIAL CHANGES found? → ESCALATE (see Step 3)
2. Do new findings increase risk? → Upgrade risk category or maintain current level
3. Do any findings decrease risk? → Consider downgrade (documented justification)
4. No material changes found → Confirm existing risk category with brief note

**Documentation:**
- Current risk category (HIGH, MEDIUM, LOW)
- Reassessed risk category (if changed)
- Justification for any risk category change
- Next refresh date per new risk category

**Manager Checkpoint:**
- [ ] Review risk assessment rationale
- [ ] Confirm risk category is appropriate for findings
- [ ] Approve risk decision and next refresh schedule

---

### Step 5: Material Change Escalation (If Applicable)

**When to Escalate:**

All material changes from Step 3 require escalation. Route to:
- **Manager:** For review and oversight (all escalations)
- **MLRO (Money Laundering Reporting Officer):** For determination of SAR-reportability (US) or regulatory reporting (UK/EU/MENA)

**Escalation Urgency:**
- **IMMEDIATE (same-day):** Sanctions designation, criminal charges, evidence of beneficial ownership concealment
- **PRIORITY (24-48 hours):** New beneficial owners, business pivots to high-risk sectors, regulatory enforcement actions
- **STANDARD (1 week):** Material ownership changes, loss of regulatory authorization, substantial adverse media

**Manager Actions:**
1. Review refresh findings and material change determination
2. Assess customer account risk and transaction history
3. Determine if SAR/suspicious activity reporting required
4. Decision: Escalate to MLRO, escalate to compliance team for investigation, or route to specialized unit

**MLRO Actions:**
1. Evaluate suspicious activity pattern (if Manager refers)
2. Determine regulatory reporting obligation
3. Determine account actions: monitoring enhancement, transaction review, account closure review
4. Document decision and rationale in case file

**Post-Escalation:**
- Account placed on enhanced monitoring pending resolution
- Next refresh scheduled after escalation resolved and account decision made

---

### Step 6: Generate Output & Schedule Next Refresh

**Output Template:** Use locked template from OUTPUT_TEMPLATES/refresh-report.md

**Refresh Report Contains:**
- [ ] Refresh initiation date and trigger
- [ ] Summary of 5 searches conducted (platforms, dates)
- [ ] Key findings from each search (new and unchanged)
- [ ] Comparison table: Original onboarding vs. refresh findings
- [ ] Material change determination (yes/no, what changed)
- [ ] Risk category re-assessment with justification
- [ ] Escalation decision and routing (if applicable)
- [ ] Manager sign-off with name, date
- [ ] MLRO referral summary (if escalated)
- [ ] Next refresh date scheduled

**Case File Updates:**
- Attach refresh report to customer case file
- Link to original onboarding findings for comparison
- Update customer profile with new information (address, beneficial owners, regulatory status)
- Update risk category and next refresh date in system

**Schedule Next Refresh:**
- HIGH risk: 12 months from refresh date
- MEDIUM risk: 24 months from refresh date (36 months for HIGH if reassessed to MEDIUM)
- LOW risk: 36 months from refresh date
- Set system reminder for 30 days before due date

**Manager Final Checkpoint:**
- [ ] Refresh report complete and accurate
- [ ] Case file updated with findings
- [ ] Next refresh date scheduled appropriately
- [ ] Escalations routed correctly (if applicable)
- [ ] Archive refresh documentation per retention requirements

---

## Material Change Examples

### Scenario 1: Business Pivot (Material Change)
**Original:** Business consulting firm, LOW risk, 3-year refresh cycle
**Refresh finds:** Company now offers crypto trading services and investment management
**Analysis:** Business pivoted to high-risk sector (crypto) without prior disclosure
**Action:** ESCALATE - Material change, risk reassessment required (likely HIGH)

### Scenario 2: Beneficial Owner Change (Material Change)
**Original:** Family-owned business, clear beneficial ownership, MEDIUM risk
**Refresh finds:** New beneficial owner acquired 30% stake via offshore entity, beneficial ownership structure now opaque
**Analysis:** Beneficial ownership changed materially, transparency decreased
**Action:** ESCALATE - Investigate new beneficial owner, determine if concealment patterns present

### Scenario 3: Regulatory Action (Material Change)
**Original:** Financial services firm with valid licenses, MEDIUM risk
**Refresh finds:** Regulatory authority issued enforcement action for compliance failures; CEO charged with fraud (media alert)
**Analysis:** Regulatory status changed; principals now under criminal investigation
**Action:** IMMEDIATE ESCALATION - Contact MLRO for SAR evaluation and account disposition

### Scenario 4: No Material Changes (Update Only)
**Original:** E-commerce business, transparent ownership, MEDIUM risk
**Refresh finds:** Address moved within same city; new CFO on board; annual revenue growth documented
**Analysis:** No material changes to beneficial ownership, business model, or regulatory status; governance updates are normal
**Action:** CONFIRM risk category, document findings, schedule next refresh per 24-month interval

---

## Regional Compliance Notes

Refresh requirements vary by jurisdiction. See detailed guidance:
- **UK/EU:** [regulations-uk-eu.md](references/regulations-uk-eu.md) - AMLD5 compliance, annual HIGH risk
- **MENA:** [regulations-mena.md](references/regulations-mena.md) - Enhanced QUARTERLY for HIGH risk per UACB/SAMA
- **US:** [regulations-us.md](references/regulations-us.md) - FinCEN CDD rule, annual HIGH risk

**Multi-Jurisdictional Customers:** Apply most stringent requirement. If customer operates in both UK and US, use annual refresh interval (both jurisdictions require annual for HIGH risk).

---

## Locked Output Template

Use: `/OUTPUT_TEMPLATES/refresh-report.md`

Ensures consistent documentation and audit trail compliance.

---

**Version:** 1.0.0
**Last Updated:** 2026-02-12
**Author:** Vyayasan
**Regulated:** AMLD5 (UK/EU), FinCEN CDD Rule (US), UACB/SAMA (MENA)

**MCP Integration:** Uses same ~~browser, ~~excel, ~~pdf connectors as onboarding workflow. See `CONNECTORS.md`.
