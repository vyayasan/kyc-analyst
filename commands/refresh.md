---
description: Periodic customer review with independent verification
argument-hint: "<customer name>"
---

# Refresh

Periodic customer review with independent verification searches to ensure ongoing due diligence compliance and identify any changes in customer risk profile or undisclosed relationships.

## Usage

```
/kyc:refresh <customer name>
```

## Process

1. **Initiate** - Verify last refresh date, confirm trigger (time-based, risk-based, event-based)
2. **Re-run Step 0** - Execute all 5 independent verification searches
3. **Compare** - Identify changes since last review (new directorships, adverse media, PEP status)
4. **Assess** - Classify changes as material or non-material
5. **Decide** - Update risk rating or escalate if material changes detected
6. **Document** - Generate refresh report, update case file, schedule next refresh

## Refresh Intervals

- **HIGH risk:** Annual (12 months)
- **MEDIUM risk:** 24 months (UK/EU), 6 months (MENA)
- **LOW risk:** 36 months (UK/EU), 12 months (MENA/US)

## HITL Checkpoints

- Analyst confirms trigger and timing before proceeding
- Manager approves search completeness
- Analyst classifies material vs non-material changes
- Manager reviews risk reassessment
- MLRO notified for immediate escalation cases

---

**Version:** 2.3.0
**Author:** Vyayasan
