---
name: transaction-monitoring
description: >
  AML transaction monitoring for ongoing customer relationships. Identifies suspicious patterns
  including structuring, layering, and unusual activity. Assesses against regulatory thresholds
  and prepares Suspicious Activity Reports (SARs) with HITL decision gates.
user-invocable: true
category: compliance
estimated-duration: 20 minutes
---

# Transaction Monitoring Skill - v1.0.0

AML transaction monitoring for ongoing customer relationships. Identifies suspicious patterns, assesses structuring and layering, and prepares Suspicious Activity Reports (SARs).

## Overview

Transaction monitoring is a continuous obligation under AML regulations. This skill analyzes transaction data to detect patterns that may indicate money laundering, terrorist financing, or other financial crime.

## Detection Patterns

### 1. Structuring (Smurfing)
- Multiple transactions just below reporting thresholds
- Multiple deposits across different branches/channels on same day
- Pattern of round-number transactions
- **Threshold (US):** $10,000 CTR threshold; $5,000 aggregated suspicious activity

### 2. Layering
- Complex routing through multiple accounts or entities
- Rapid movement between accounts with no clear business purpose
- International transfers through multiple jurisdictions
- Use of shell companies or nominee accounts

### 3. Circular Flows
- Money leaving and returning to same account via intermediaries
- Round-trip transactions with no economic substance
- Funds flowing through subsidiaries back to parent

### 4. Velocity Anomalies
- Sudden increase in transaction frequency
- Dramatic change in average transaction value
- Activity inconsistent with customer profile or declared business
- Dormant account reactivation with high-value activity

### 5. Geographic Risk Patterns
- Transactions to/from FATF grey-list or black-list jurisdictions
- Unexplained payments to/from high-risk countries
- Wire transfers to known shell company jurisdictions

## Monitoring Process

### Step 1: Data Analysis
- Import transaction data (CSV, Excel, or database extract)
- Calculate baseline metrics (average value, frequency, counterparties)
- Identify deviations from customer profile

### Step 2: Pattern Detection
- Apply detection rules for each pattern type
- Flag transactions meeting alert criteria
- Score alerts by severity (LOW/MEDIUM/HIGH/CRITICAL)

### Step 3: Investigation [HITL Checkpoint]
- Analyst reviews flagged transactions
- Assesses whether activity has legitimate explanation
- Researches counterparties and destinations
- Documents investigation findings

### Step 4: Decision
- **CLEAR:** Document rationale, close alert
- **SUSPICIOUS:** Draft SAR narrative, escalate to MLRO
- **CRITICAL:** Immediate MLRO notification, consider account freeze

### Step 5: SAR Preparation (if applicable)
Claude drafts SAR narrative including:
- Subject information
- Suspicious activity description
- Transaction details
- Why activity is suspicious
- Supporting evidence

**CRITICAL HITL: SAR filing is always a human decision. Claude drafts; MLRO reviews and files.**

## Output

- Transaction analysis report (Excel with flagged items)
- Alert summary with severity scoring
- SAR draft (if suspicious activity identified)
- Escalation brief for MLRO
- Updated customer risk assessment

## Regulatory Basis

- **US:** BSA/AML, FinCEN SAR requirements ($5,000 threshold)
- **UK/EU:** AMLD5 ongoing monitoring, POCA 2002 SAR obligations
- **MENA:** CBUAE, SAMA transaction monitoring requirements

---

**Version:** 1.0.0
**Author:** Vyayasan
