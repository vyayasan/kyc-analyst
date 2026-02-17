# KYC Analyst — Sandbox

**Branch:** `claude/explore-multilingual-identity-verification-DaUet`

Private sandbox directory on a feature branch for testing ideas before they go into main.
Nothing in `sandbox/` should be merged to main without review.

## Active Explorations

### 1. Multilingual Identity Verification (`docs/exploration/`)
- Cohere Tiny Aya integration for name transliteration and non-English document processing
- Selfie + document scan with deepfake mitigation strategy
- See [`docs/exploration/multilingual-identity-verification.md`](docs/exploration/multilingual-identity-verification.md)

### 2. Proof of Concepts (`poc/`)
- `poc/tiny-aya-transliteration/` — Name transliteration accuracy test against OFAC SDN
- `poc/mrz-parsing/` — MRZ field extraction from passport images

## Structure

```
sandbox/
├── docs/exploration/     # Written explorations and analysis
├── poc/                  # Proof-of-concept code
│   ├── tiny-aya-transliteration/
│   └── mrz-parsing/
└── benchmarks/           # Test data and results
```
