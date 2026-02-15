# Changelog

All notable changes to the KYC Analyst plugin are documented here.

## [2.3.0] - 2026-02-12 (Current Release)

### Added
- MCP Integration Guide for Claude in Chrome, fpdf2, openpyxl
- Connector flexibility system (`~~placeholder` syntax for tool-agnostic integrations)
- 5 complete example cases with inputs and expected outputs
- Output templates locked (PDF 17-section, Excel 4-sheet, Case Folder 6-part)
- Workflow templates for 5 common scenarios (copy-paste ready)

### Changed
- Locked all output formats — consistent structure across all cases
- Improved risk scoring precision for edge cases between bands
- Enhanced Step 0 search coverage to 72+ sources across 6 categories

### Fixed
- fpdf2 Unicode bug: replaced checkmarks with `[OK]`/`[X]` for Helvetica compatibility
- fpdf2 deprecation: migrated from `ln=True` to `new_x="LMARGIN", new_y="NEXT"`
- Excel `===` serialisation bug with Desktop Commander

## [2.2.0] - 2026-02-01

### Added
- Auto case folder creation (numbered 001-006 structure)
- Immutable audit trail template (AUDIT_TRAIL.md)
- Case folder structure template locked

### Changed
- PDF report structure finalised at 17 sections
- Excel dashboard locked at 4 sheets (Summary, Directorships, Discrepancies, Risk)

## [2.1.0] - 2026-01-15

### Added
- Interactive onboarding mode (`/kyc:onboard-interactive`)
- Excel 4-sheet dashboard generation via openpyxl
- Quick Start Guide (10-minute walkthrough)

### Changed
- Improved document extraction prompting for passports and utility bills
- Enhanced PEP screening with OpenSanctions 100+ country coverage

## [2.0.0] - 2026-01-01

### Added
- Step 0 Independent Verification framework (mandatory pre-onboarding)
- 6 mandatory Step 0 search categories (Adverse Media, ICIJ, Directorships, PEP, Professional, Sanctions)
- 17 stagegate HITL enforcement model
- 4-factor deterministic risk scoring (Geographic 30%, Customer 35%, Product 25%, Channel 10%)
- PDF report generation via fpdf2

### Changed
- Complete rewrite of onboarding workflow (onboard.md: 1,047 lines)
- Risk bands standardised: LOW (0-20), MEDIUM (21-60), HIGH (61-80), CRITICAL (81-100)

## [1.0.0] - 2025-11-01

### Added
- Initial release
- Basic KYC onboarding workflow
- Sanctions screening (OFAC, UN, EU, UK)
- Companies House search
- Simple risk calculation
- Basic text-based reporting
