# Refresh Trigger Library

Complete decision tree for when to trigger customer refresh outside normal schedule.

## Time-Based Triggers

**Annual Refresh (All HIGH risk)**
- Automatic refresh on anniversary of last onboarding or refresh
- Compliance requirement across all jurisdictions (UK, MENA, US)
- Document: Time-based refresh scheduled per risk category

**Periodic Schedule**
- HIGH: Annual (every 12 months)
- MEDIUM: 24 months (every 2 years for UK/EU, semi-annual for MENA)
- LOW: 36 months (every 3 years, annual for MENA)
- Default: Next refresh date auto-calculated at end of each refresh

## Risk-Based Triggers

**Customer Risk Assessment Changes**
- Risk score increases (e.g., LOW to MEDIUM, MEDIUM to HIGH)
- Regulatory classification changes (from standard to PEP, beneficial owner, correspondent bank)
- When triggered: Immediate refresh to validate new risk assessment

**Business Model Red Flags**
- Customer transitions to high-risk sector (crypto, gambling, trade finance, weapons)
- Transaction patterns show sudden increase in volume/complexity
- New beneficial owners enter picture
- Corporate restructuring or ownership concentration

**Behavioral Anomalies**
- Transaction patterns diverge significantly from profile
- First time transacting with high-risk jurisdictions
- Cyclical activity patterns emerging (sign of structuring or layering)
- Large transactions after period of inactivity

## Event-Based Triggers

### External Events

**Regulatory Actions**
- Customer appears on government sanctions list (OFAC, EU, UN)
- Customer receives regulatory enforcement action, license revocation, or criminal charges
- Customer's industry faces new regulatory restrictions
- When triggered: Immediate escalation (same-day response required)

**Adverse Media Detection**
- Media coverage linking customer to:
  - Money laundering, terrorist financing, or corruption
  - Regulatory enforcement or investigation
  - Criminal activity
  - PEP designation or government position
- When triggered: Within 24 hours of alert, determine if material change

**Market Intelligence**
- Industry reports identifying customer's sector as emerging risk
- Beneficial owner identified in sanctions-related investigation
- Corporate news: M&A, restructuring, bankruptcy filing
- Negative financial indicators: debt covenant breach, credit rating downgrade

### Internal Events

**Compliance Escalations**
- Transaction monitoring alert routed to MLRO suggesting SAR-reportable activity
- Customer subject of internal investigation
- Prior escalation period concluded, requiring revalidation
- When triggered: Refresh integrated into escalation resolution process

**Customer Contact/Application**
- Customer requests new service or product line
- Customer applies for higher transaction limits or different currency access
- Customer initiates account restructuring or closing
- When triggered: Refresh to baseline new service risk before approval

**System Alerts**
- Database reconciliation identifies missing or inconsistent data
- Third-party data provider flags customer record change
- PEP/sanctions database updates affecting customer or family members
- When triggered: Within 5 business days of alert

## Material Change Thresholds

**Immediate Escalation Required (Same-day)**
- Sanctions designation
- Evidence of criminal conviction or investigation
- Beneficial ownership concealment discovered
- Emergence of PEP status not previously disclosed

**High Priority Escalation (24-48 hours)**
- New beneficial owner of 25%+ stake
- Business pivot to high-risk sector
- Regulatory enforcement action against customer or related party
- Adverse media with verified sources

**Standard Escalation (1 week)**
- Address change outside documented geographic scope
- New business line requiring new due diligence
- Risk score upgrade warranting new procedures
- Material change to beneficial ownership structure (non-concealment)

**Update Only (No escalation)**
- Address change within expected geography
- Standard corporate governance changes (board updates, officer rotations)
- Beneficial ownership updates confirming prior findings
- Risk score downgrade based on positive developments

## Trigger Documentation

Every refresh must record:
1. **Trigger Type:** Time-based, risk-based, or event-based
2. **Trigger Date:** When condition identified
3. **Trigger Description:** Specific rationale (e.g., "Annual refresh - HIGH risk", "Sanctions media alert", "Customer requested new service")
4. **Refresh Decision:** Scheduled refresh, immediate refresh, or escalation
5. **Urgency Level:** Routine, priority, or immediate
6. **Justification:** Regulatory requirement or risk management rationale

## Automation Guidance

**Auto-triggered Refreshes:**
- Schedule next refresh date at end of each completed refresh
- Monthly system check for overdue refreshes (risk category + last refresh date)
- Escalate overdue refreshes to manager for scheduling

**Alert-driven Refreshes:**
- Sanctions database matches: flag immediately
- Adverse media matches: analyst review within 24 hours
- MLRO escalation closure: trigger refresh before account reactivation
