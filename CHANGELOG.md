# Changelog

All notable changes to the **What to Use When** skill are documented here.
This project adheres to [Semantic Versioning](https://semver.org/).

## [1.0.0] - 2026-07-24

First public release (renamed from the internal `cowork-cost-guard` prototype).

### Added
- Renamed the skill to **`what-to-use-when`** with the friendly display name **"What to Use When"**
  and a `Compass` logo icon.
- Precedence rule so the skill runs **FIRST — before any thinking, retrieval, task creation, or file
  generation** — and takes priority over action-bias / gather-before-generate.
- Explicit, separately-called trigger conditions for: summarizing email, meetings, and Teams messages
  (over any window); "catch me up" / "what did I miss"; single questions and calendar/contact/people
  lookups; billing/licensing questions; drafting a document; building a deck or spreadsheet; deep
  research; and data analysis.
- Routing table mapping each task type to the right included capability (Copilot Chat; Copilot in
  Word/Excel/PowerPoint; Researcher; Analyst; specialized 1P agents) or to Cowork for multi-output work.
- One-click hand-off link to Microsoft 365 Copilot Chat (`https://m365.cloud.microsoft/chat/`).
- GitHub repository packaging: README with end-user and organization deployment guides, MIT license,
  contributing guide, logo, and validation/test reports.

### Changed
- **Removed all pricing** from user-facing output (no credits, dollar amounts, or estimates) so the
  skill is safe to share with customers.
- Reworked the exclusions so **direct M365 actions** (send/schedule/post/create) and **multi-step,
  multi-output jobs** are never gated.
- Compressed the description to a folded scalar within Cowork's **1,024-character** (JSON-escaped)
  limit so the skill can be shared/published without validation errors.

### Validation
- Static quality score: **98/100 (Excellent)**.
- Independent-judge trigger tests: **100% recall / 100% precision**, no flaky triggers (see
  `reports/`). Results are simulations, not a live-router guarantee.
