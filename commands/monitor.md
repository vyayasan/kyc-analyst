---
description: AML transaction monitoring and suspicious activity reporting
argument-hint: "<customer name or account>"
---

# Monitor

AML transaction monitoring for ongoing customer relationships, identifying suspicious patterns and generating Suspicious Activity Reports (SARs) when required.

## Usage

```
/kyc:monitor <customer name or account>
```

## Monitoring Scope

- Transaction pattern analysis (structuring, layering, circular flows)
- Velocity anomaly detection (high-frequency, high-value patterns)
- Beneficial ownership changes
- Jurisdiction risk changes (new high-risk country flows)
- Adverse media developments
- Sanctions list updates

## Detection Patterns

- **Structuring:** Multiple transactions just below reporting thresholds
- **Layering:** Complex routing through multiple accounts/entities
- **Circular Flows:** Money cycling back to origin
- **Velocity Anomalies:** Sudden increase in transaction frequency/value
- **Geographic Risk:** Transactions to/from high-risk jurisdictions

## Output

- Transaction analysis report
- SAR draft (if suspicious activity identified)
- Escalation narrative for MLRO
- Updated risk assessment

## HITL Checkpoint

SAR filing decisions always require MLRO review and approval. Claude drafts the SAR; the human files it.

---

**Version:** 2.3.0
**Author:** Vyayasan
