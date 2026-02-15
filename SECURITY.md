# Security Policy

## Reporting a Vulnerability

If you discover a security vulnerability in this plugin, **do NOT open a public GitHub issue.**

Instead, please report it privately:
- LinkedIn DM: [Sandipanee Samantaray](https://linkedin.com/in/sandipanee)

### What to Include
- Description of the vulnerability
- Steps to reproduce
- Potential impact
- Suggested fix (if you have one)

### Response Time
- Acknowledgment: Within 48 hours
- Assessment: Within 7 days
- Fix (if confirmed): Within 14 days

## Scope

This security policy covers:
- The plugin code (commands, skills, templates)
- The risk scoring methodology
- The audit trail format
- Data handling in workflows

This security policy does NOT cover:
- Claude Cowork itself (report to Anthropic)
- Third-party data sources (OFAC, Companies House, etc.)
- Your own deployment environment

## Data Handling

This plugin:
- Processes all data locally within Claude Cowork
- Does NOT send data to external servers (beyond the public APIs it queries)
- Does NOT store data outside your local Cowork environment
- Does NOT have network access beyond what Claude Cowork provides

## Known Considerations

1. **Public API queries are not encrypted end-to-end** — Companies House, OFAC, and sanctions list queries go over HTTPS but the query content (entity names) is visible to those services.
2. **Audit trail logs contain entity names** — Secure your local case folders appropriately.
3. **Excel/PDF outputs contain PII** — Handle generated reports per your firm's data classification policy.

## Supported Versions

| Version | Supported |
|---------|-----------|
| 2.3.x   | Yes       |
| < 2.3   | No        |
