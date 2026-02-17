# Exploration: Multilingual Identity Verification

**Date:** 2026-02-17
**Status:** Exploration / Pre-RFC
**Author:** Vyayasan

---

## Context

Two related ideas surfaced from pilot feedback and industry developments:

1. **Cohere's Tiny Aya models** (launched 2026-02-17) — open-weight multilingual models covering 70+ languages. Regional variants for Africa, South Asia, and Asia-Pacific/Europe. Runs on-device at 3.35B parameters.

2. **Selfie + document scan verification** — requested by pilot users. Timely given that Veriff (used by Griffin for selfie + doc verification) was recently compromised by deepfake attacks. Griffin reportedly replacing them with another supplier.

Both point toward the same gap: KYC Analyst v1.0.0 handles English-language public-source verification well, but has no support for (a) non-English name matching / document processing, or (b) biometric identity verification.

---

## Idea 1: Cohere Tiny Aya for Multilingual KYC

### What Tiny Aya Is

- **3.35B parameter** open-weight multilingual models
- **70+ languages** including South Asian (Hindi, Bengali, Tamil, Urdu, Gujarati, Telugu, Marathi, Punjabi), African, and Asia-Pacific/European languages
- **Regional variants:** TinyAya-Earth (Africa), TinyAya-Fire (South Asia), TinyAya-Water (APAC/Europe)
- **Runs on-device** — laptop-grade hardware, no internet required
- **Open-weight** — available on HuggingFace, Kaggle, Ollama
- **Trained on 64x H100s** — modest compute, reproducible

### Where This Fits in KYC Analyst

The README already acknowledges: *"Comprehensive multilingual name matching requires specialized tooling."* Current approach is manual: analysts add romanization aliases by hand.

Tiny Aya could close specific gaps:

| Gap | How Tiny Aya Helps | Feasibility |
|-----|-------------------|-------------|
| **Name transliteration** | Arabic/Cyrillic/Devanagari names to Latin script and back. Critical for sanctions matching — OFAC SDN has alternate spellings but not all scripts. | High — this is core multilingual capability |
| **Adverse media in local languages** | Translate search results from non-English news sources. A PEP in Dubai may have Arabic-language coverage that English searches miss entirely. | High — translation is a primary use case |
| **Document field extraction** | Parse non-English identity documents (utility bills, bank statements, company registrations) where field labels are in local language. | Medium — needs evaluation against doc types |
| **Jurisdiction expansion** | APAC and LatAm jurisdiction packs (on roadmap) require non-English capability by definition. | High — enabler for planned roadmap items |
| **Offline/air-gapped deployment** | Compliance teams in regulated environments may need on-premise processing of non-English text without sending data to external APIs. | High — on-device is a differentiator |

### Architecture Fit

KYC Analyst runs on Claude (which handles reasoning, workflow, stagegates). Tiny Aya would slot in as a **specialized MCP tool** for multilingual text processing:

```
Claude (reasoning + workflow)
    ↓
MCP Connector: tiny-aya-multilingual
    ↓
Local Tiny Aya model (via Ollama or direct inference)
    ↓
Returns: transliterated names, translated text, extracted fields
```

This keeps the architecture clean — Claude orchestrates, Tiny Aya handles the multilingual heavy lifting that a general-purpose LLM may not do reliably for low-resource languages.

### What to Evaluate

1. **Name transliteration accuracy** — test against OFAC SDN alternate name lists. How does Tiny Aya compare to dedicated transliteration libraries (e.g., ICU, Transliterate)?
2. **Regional variant selection** — do we bundle all three (Earth/Fire/Water) or let users pick based on their jurisdiction focus?
3. **Sanctions matching recall** — does adding Tiny Aya transliteration catch matches that the current English-only approach misses? (This is the key metric.)
4. **Latency** — on-device inference at 3.35B params should be fast, but verify it doesn't slow down the Step 0 flow.
5. **Licensing** — confirm the open-weight license is compatible with MIT.

### Suggested Next Step

Build a proof-of-concept MCP connector that:
- Takes a name in any script + target script
- Returns transliterated variants
- Test against 50 names from OFAC SDN with known alternate spellings
- Measure recall improvement vs. current English-only approach

---

## Idea 2: Selfie + Document Scan with Deepfake Mitigation

### The Problem

Pilot users want selfie + document verification (selfie holding passport, liveness check, face match). This is standard in regulated KYC — banks, fintechs, and exchanges all require it.

But the landscape is hostile:

- **Veriff** (used by Griffin and many fintechs for selfie + doc) was recently beaten by deepfake attacks
- **Trend Micro research** demonstrated bypassing Veriff's liveness checks by streaming deepfaked faces onto an Android Cloud service
- **Underground services** advertise Veriff/Onfido/Jumio/Sumsub bypass for ~$30 per identity, or ~$180-200 for exchange KYC
- **Gartner (Feb 2024):** By 2026, 30% of enterprises will consider biometric identity verification unreliable *in isolation* due to AI-generated deepfakes
- **Veriff's own data:** 46% YoY increase in adversary-in-the-middle attacks, many using real-time deepfakes
- Griffin reportedly replacing Veriff with another supplier following the incident

### Why This Matters for KYC Analyst

KYC Analyst's current value proposition is *analyst-in-the-loop verification using free public sources*. Adding selfie + doc verification would:

1. **Close the biggest feature gap** — it's the most common pilot user request
2. **Complement, not replace** the existing approach — Step 0 independent verification catches things biometrics can't (adverse media, sanctions history, PEP status)
3. **Differentiate** — if we build it with deepfake awareness from day one, we avoid the Veriff-style vulnerability

### Deepfake Mitigation: Multi-Layer Approach

Single-factor biometric verification is broken. The answer isn't better liveness detection alone — it's **layered verification** where no single factor is trusted in isolation.

**Layer 1: Document Authenticity (before any biometric)**
- MRZ (Machine Readable Zone) parsing and cross-check
- Document template matching (is this a real UK passport layout?)
- Security feature detection (holograms, watermarks — limited by camera quality)
- NFC chip reading where available (e-passports)
- Cross-reference extracted data against declared information

**Layer 2: Liveness + Face Match (with deepfake awareness)**
- Passive liveness detection (texture analysis, reflection patterns)
- Active liveness challenges (random head movements, expressions)
- Injection attack detection (is the camera feed real or a virtual camera?)
- Device integrity checks (is this a real device or an emulator/cloud VM?)
- Environmental signals (lighting consistency, background plausibility)

**Layer 3: Behavioural + Contextual Signals (KYC Analyst's strength)**
- Does the selfie match the person described in Step 0 findings?
- Is the document country consistent with declared nationality?
- Device geolocation vs. declared residence
- Session behaviour analysis (timing, interaction patterns)
- Cross-reference against existing case data

**Layer 4: Independent Verification (existing Step 0)**
- The existing 5+1 searches provide context that pure biometric providers lack
- A deepfake can fool a camera but can't fabricate a Companies House directorship history
- Adverse media and sanctions checks provide orthogonal verification

### Build vs. Buy vs. Integrate

| Approach | Pros | Cons |
|----------|------|------|
| **Build from scratch** | Full control, deepfake-aware from day one, no vendor dependency | Massive scope, needs ML expertise, ongoing arms race |
| **Integrate open-source** | Community-maintained, inspectable, cost-effective | Fragmented ecosystem, integration burden, may lag behind attack evolution |
| **Integrate commercial provider** | Battle-tested, handles the arms race, compliance-certified | Vendor lock-in, cost, single point of failure (the Veriff problem) |
| **Hybrid: open-source + commercial fallback** | Best of both, defence in depth | Complexity, two integration surfaces |

**Recommended approach for v2:** Start with **document verification only** (Layer 1) using open-source OCR/MRZ parsing, and **defer biometric liveness** to a commercial provider that can be swapped (the Griffin lesson). KYC Analyst's architecture already supports this via MCP connectors — the biometric provider is just another connector.

### What to Evaluate

1. **Open-source document verification:** Evaluate Tesseract OCR, PassportEye (MRZ parsing), and DocTR for document field extraction
2. **Deepfake detection models:** Evaluate open-source options (Microsoft FaceAnalyzer, SenseTime Anti-Spoof) for liveness checks
3. **Provider landscape post-Veriff:** Research which providers are gaining traction as alternatives (iProov, Onfido, Sumsub, Microblink, GBG)
4. **Regulatory requirements:** Which jurisdictions mandate biometric verification vs. accept document-only? (UK FCA doesn't mandate selfie; some MENA regulators do)
5. **Privacy implications:** Biometric data is special category under GDPR/UK DPA. Storage, processing, and retention rules are strict.

### Suggested Next Step

Build a proof-of-concept for **document-only verification** (no biometrics):
- MRZ parsing from passport photo
- Cross-reference extracted name/DOB/nationality against declared customer info
- Flag discrepancies at an existing stagegate
- This adds value immediately without entering the deepfake arms race

---

## How These Two Ideas Connect

Multilingual capability and document verification reinforce each other:

- Non-English identity documents need multilingual OCR/field extraction (Tiny Aya)
- Name transliteration improves sanctions matching for customers verified via document scan
- APAC/MENA jurisdiction expansion (roadmap) requires both capabilities

A reasonable sequencing:

```
v1.1  Multilingual name transliteration (Tiny Aya MCP connector)
      → Immediate improvement to sanctions matching recall
      → Enables APAC/LatAm jurisdiction packs

v1.2  Document verification — MRZ parsing + field extraction
      → Closes the biggest pilot user gap (doc scan)
      → Uses Tiny Aya for non-English documents
      → No biometric data, no deepfake risk

v2.0  Biometric liveness (commercial provider via MCP connector)
      → Swappable provider (learned from Griffin/Veriff)
      → Layered with existing Step 0 verification
      → Deepfake mitigation via multi-layer approach, not single-factor trust
```

---

## References

- [Cohere Launches Tiny Aya — TechCrunch](https://techcrunch.com/2026/02/17/cohere-launches-a-family-of-open-multilingual-models/)
- [Cohere Tiny Aya for 70+ Languages — Dataconomy](https://dataconomy.com/2026/02/17/cohere-launches-tiny-aya-multilingual-ai-models-for-70-languages/)
- [Cohere Multilingual Models — VentureBeat](https://venturebeat.com/ai/cohere-launches-new-ai-models-to-bridge-global-language-divide)
- [Griffin Partners with Veriff for ID&V](https://griffin.com/blog/griffin-partners-with-veriff-to-offer-idv-to-baas-customers)
- [Trend Micro: Deepfakes and eKYC](https://www.trendmicro.com/vinfo/us/security/news/cyber-attacks/ai-vs-ai-deepfakes-and-ekyc)
- [Gartner: 30% of Enterprises Will Distrust Biometric Verification by 2026](https://www.gartner.com/en/newsroom/press-releases/2024-02-01-gartner-predicts-30-percent-of-enterprises-will-consider-identity-verification-and-authentication-solutions-unreliable-in-isolation-due-to-deepfakes-by-2026)
- [Veriff Identity Fraud Report 2026](https://www.veriff.com/pr-news/veriff-identity-fraud-report-2026)
- [Deepfakes and Authentication in 2026 — Keyless](https://keyless.io/blog/post/deepfakes-in-2026-what-s-real-what-s-hype-)
