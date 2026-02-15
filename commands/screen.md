---
description: Comprehensive sanctions and PEP screening
argument-hint: "<customer name>"
---

# Screen

Comprehensive sanctions screening against OFAC, EU, UK, and UN lists, plus PEP screening against international politically exposed persons databases.

## Usage

```
/kyc:screen <customer name>
```

## Screening Targets

- Individual customers
- Beneficial owners and UBOs
- Company directors and officers
- Shareholders (25%+ ownership)
- Family members and close associates (for PEP cases)

## Screening Sources (12+)

**Sanctions Lists:**
- OFAC SDN (Specially Designated Nationals)
- EU Consolidated Sanctions List
- UK HM Treasury Sanctions List
- UN Consolidated Sanctions List
- Interpol Red/Yellow Notices

**PEP Databases:**
- EveryPolitician
- Wikidata political figures
- UK Parliament Register of Interests
- CIA World Factbook leadership
- National electoral commission databases

**Additional:**
- OpenSanctions
- UK Court records
- Companies House insolvencies

## False Positive Assessment

When a potential match is found:
1. Compare name similarity (exact match vs partial)
2. Compare date of birth (if available)
3. Compare nationality and location
4. Assess context and distinguishing factors
5. Document decision: TRUE MATCH or FALSE POSITIVE

## HITL Checkpoint

All matches (even likely false positives) require analyst review and sign-off before proceeding.

---

**Version:** 1.0.0
**Author:** Vyayasan
