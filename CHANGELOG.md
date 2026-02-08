# Changelog

All notable changes to Attest are documented here. Format follows [Keep a Changelog](https://keepachangelog.com/).

## [1.2.0] - 2026-02-08

### Fixed
- Information questions (who, what, describe) now prompt for free text instead of showing Confirmed/Flagged/Escalated/N/A options that don't fit the question type
- All 5 baseline organisational context questions classified as information questions

### Added
- Question Response Types section in question-frameworks skill: verification (status options) vs information (free text)
- Step 9 of review command now uses the correct response mechanism based on question type
- Classification guidance for category-specific questions

## [1.1.0] - 2026-02-08

### Fixed
- Question count ranges now accommodate 5 mandatory baseline questions at all risk levels (Low: 5-7, Medium: 6-10, High: 8-12, Critical: 12-16)
- SHA-256 hash added to output fingerprint across all files (review command, decision-logging skill, review-methodology skill, decision-log template, escalation-record template)
- Plugin manifest (plugin.json) now lists all 7 commands and skills directory
- Question presentation order made concrete: present all questions first, then collect responses one at a time
- README now documents decision log integrity limitations (not tamper-proof, self-declared identity, point-in-time approvals)

### Changed
- Risk classification strengthened: DPAs, contracts, and binding agreements default to Critical (not High)
- Reviewer identity, overall decision, and sign-off statement marked MANDATORY in review and log commands
- Filename formats enforced with explicit examples and "do NOT" warnings for wrong patterns
- Escalation command now suggests domain-appropriate role first (e.g., DPO for data protection items)
- Escalation rationale capture marked mandatory (no auto-generation)
- Disclaimer footer text included inline in review, log, and escalate commands for consistency

## [1.0.0] - 2026-02-08

### Added
- Initial build of Attest plugin (18 files)
- Plugin manifest (.claude-plugin/plugin.json)
- 7 commands: review, log, escalate, resolve, status, config, help
- 5 skills: review-methodology, risk-classification, question-frameworks, decision-logging, escalation-framework
- 3 templates: decision-log, escalation-record, review-summary
- README with installation, usage, and disclaimer
- Apache 2.0 license

### Tested
- Smoke test 1 (v1.0.0): identified issues with risk classification, filename format, missing reviewer prompts, incomplete baseline questions
- Smoke test 2 (v1.0.1): all fixes confirmed working. Critical classification, correct filename, reviewer identity/decision/sign-off prompted, all 5 baseline questions present
- Peer review: identified 6 instruction clarity issues, 7 PRD-implementation gaps, 8 audit artefact risks. 5 priority fixes applied in v1.1.0.
