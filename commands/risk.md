---
description: Risk reassessment with updated due diligence
argument-hint: "<customer name>"
---

# Risk

Comprehensive risk reassessment using four-factor heuristic model with updated due diligence requirements based on current risk profile.

## Usage

```
/kyc:risk <customer name>
```

## Risk Factors

| Factor | Weight | Description |
|--------|--------|-------------|
| Geographic Risk | 30% | Customer jurisdiction, transaction countries, wealth origin |
| Customer Risk | 35% | PEP status, industry, source of wealth clarity, complexity |
| Product Risk | 25% | Account type, expected activity, transaction volume |
| Channel Risk | 10% | Onboarding method, documentation quality |

## Risk Bands

| Band | Score Range | Action Required |
|------|-------------|-----------------|
| LOW | 0-20 | CDD sufficient, analyst approval |
| MEDIUM | 21-60 | Enhanced monitoring, senior analyst review |
| HIGH | 61-80 | EDD required, manager + MLRO approval |
| CRITICAL | 81-100 | Immediate escalation, senior management decision |

## Deterministic Scoring

The risk score is calculated mathematically from objective inputs. Same inputs always produce the same score. This ensures:
- Reproducibility across analysts
- Fairness across customers
- Auditability for regulators
- Consistency across cases

## HITL Checkpoint

Risk rating assignment requires analyst review and sign-off. Automated scoring informs but does not replace human judgment.

---

**Version:** 1.0.0
**Author:** Vyayasan
