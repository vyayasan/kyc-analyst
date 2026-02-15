---
name: screening
description: >
  Comprehensive sanctions and PEP screening against 12+ databases (OFAC, EU, UK, UN, INTERPOL)
  with false positive assessment, HITL decision gates, and regulatory-compliant documentation.
user-invocable: true
category: compliance
estimated-duration: 15 minutes
---

# Screening Skill - v2.3.0

Comprehensive sanctions and PEP screening with multi-database search, false positive assessment, and HITL decision gates.

## Overview

Screening is a mandatory component of all KYC workflows. This skill provides standalone screening capability for ad-hoc checks, batch processing, and integration into onboarding/refresh workflows.

## Screening Databases (12+ Sources)

### Sanctions Lists
1. **OFAC SDN** - US Specially Designated Nationals
2. **EU Consolidated Sanctions List** - European Union
3. **UK HM Treasury** - UK Financial Sanctions
4. **UN Consolidated List** - United Nations Security Council
5. **Interpol** - Red and Yellow Notices
6. **OpenSanctions** - Open-source aggregated sanctions data

### PEP Databases
7. **EveryPolitician** - Global political figures
8. **Wikidata** - Political and public figures
9. **UK Parliament** - Register of Members' Interests
10. **CIA World Factbook** - National leadership
11. **Electoral Commission databases** - Candidates and office holders

### Criminal/Legal
12. **UK Court records** - Criminal convictions, CCJs
13. **Companies House** - Insolvency records, disqualified directors

## Screening Process

### Step 1: Identify Screening Targets
- Customer (individual or entity)
- All beneficial owners (>25% threshold)
- Directors and senior management (entities)
- Family members and close associates (PEP cases)

### Step 2: Execute Searches
For each target, search against all applicable databases:
- Record search date, platform, and search terms
- Document all matches (including potential false positives)
- Screenshot or save evidence

### Step 3: False Positive Assessment [HITL Checkpoint]
When a potential match is found:

| Factor | Assessment |
|--------|-----------|
| Name similarity | Exact / Partial / Common name |
| Date of birth | Match / Mismatch / Unknown |
| Nationality | Match / Mismatch |
| Location | Match / Mismatch |
| Photograph | Match / Mismatch / Not available |
| Context | Supports match / Against match |

**Decision:**
- TRUE MATCH: Immediate escalation to Manager + MLRO
- FALSE POSITIVE: Document reasoning and evidence, proceed
- UNCERTAIN: Escalate for senior review

### Step 4: Generate Report
- Screening summary with all targets and results
- False positive assessment documentation (if applicable)
- Escalation brief (if true match or uncertain)
- Recommendations and next steps

## Batch Screening

For processing multiple alerts:
```
Analyze [X] screening alerts from uploaded CSV.
For each alert:
- Assess match quality
- Check for false positive patterns
- Research as needed
- Provide recommendation (CLEAR/ESCALATE)
Create Excel report with all analyses.
```

## Regulatory Basis

- OFAC compliance (US)
- EU Sanctions Regulations
- UK Money Laundering Regulations 2017
- UN Security Council Resolutions
- AMLD5 screening requirements

---

**Version:** 2.3.0
**Author:** Vyayasan
