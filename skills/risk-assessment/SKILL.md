---
name: risk-assessment
description: >
  Deterministic heuristic risk scoring using a four-factor weighted model (Geographic 30%,
  Customer 35%, Product 25%, Channel 10%) aligned with Basel III, EBA Guidelines, FATF standards,
  and FinCEN guidance. Bands: LOW (0-20), MEDIUM (21-60), HIGH (61-80), CRITICAL (81-100).
user-invocable: true
category: compliance
estimated-duration: 10 minutes
---

# Risk Assessment Skill - v2.3.0

Deterministic heuristic risk scoring using a four-factor weighted model aligned with Basel III, EBA Guidelines, FATF standards, and FinCEN guidance.

## Overview

Risk assessment is performed during onboarding and refresh to classify customers into risk bands that determine the level of due diligence required and ongoing monitoring frequency.

## Four-Factor Risk Model

### Factor 1: Geographic Risk (30% Weight)

| Indicator | Score Range |
|-----------|------------|
| UK/EU/US/developed economy | 5-15 |
| Mid-tier economies | 20-40 |
| FATF grey-list jurisdictions | 50-70 |
| High-risk/sanctioned jurisdictions | 80-100 |
| Multiple jurisdictions with offshore | +10-20 |

**Assessed for:** Customer residence, nationality, transaction destinations, wealth origin, business operations.

### Factor 2: Customer Risk (35% Weight)

| Indicator | Score Range |
|-----------|------------|
| Salaried employee, standard profile | 5-15 |
| Self-employed, professional | 20-35 |
| Business owner, HNWI | 40-60 |
| PEP (any tier) | 60-80 |
| Complex structures, unclear ownership | 70-90 |
| Adverse media findings | +20-40 |

**Assessed for:** Occupation, PEP status, source of wealth clarity, business complexity, directorships, adverse media.

### Factor 3: Product Risk (25% Weight)

| Indicator | Score Range |
|-----------|------------|
| Personal current/savings account | 5-15 |
| Investment/wealth management | 20-40 |
| Trade finance, correspondent banking | 50-70 |
| Virtual assets, high-value transactions | 60-80 |
| Complex structured products | 70-90 |

**Assessed for:** Account type, expected activity, transaction volume, product complexity.

### Factor 4: Channel Risk (10% Weight)

| Indicator | Score Range |
|-----------|------------|
| Face-to-face, standard onboarding | 5-10 |
| Remote/digital onboarding with verification | 15-25 |
| Intermediary-introduced | 30-50 |
| Anonymous/pseudonymous channels | 70-90 |

**Assessed for:** Onboarding method, documentation quality, intermediary involvement.

## Risk Score Calculation

```
Total Score = (Geographic x 0.30) + (Customer x 0.35) + (Product x 0.25) + (Channel x 0.10)
```

## Risk Bands and Required Actions

| Band | Score | Due Diligence | Approval Level | Monitoring |
|------|-------|---------------|----------------|------------|
| LOW | 0-20 | Standard CDD | Analyst | 3-5 year review |
| MEDIUM | 21-60 | Enhanced monitoring | Senior Analyst | 1-2 year review |
| HIGH | 61-80 | Full EDD | Manager + MLRO | 6-12 month review |
| CRITICAL | 81-100 | Immediate escalation | Senior Management | Quarterly or reject |

## Determinism Guarantee

The risk score is deterministic:
- Same inputs always produce the same score
- No subjective judgment in calculation
- Mathematical formula applied consistently
- Ensures fairness and reproducibility
- Auditable by regulators

## HITL Checkpoint

While the score is calculated automatically, the analyst must:
1. Review the calculated score
2. Confirm the input factors are accurate
3. Sign off on the risk classification
4. Approve or challenge the recommended action

The human always has final say on risk classification.

## Escalation Triggers

Automatic escalation regardless of score:
- PEP status identified
- Sanctions match (true or uncertain)
- Material misrepresentation detected
- Source of wealth/funds unexplained
- Multiple high-risk indicators combined

---

**Version:** 2.3.0
**Author:** Vyayasan
