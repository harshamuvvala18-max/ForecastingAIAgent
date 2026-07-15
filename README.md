# AI Connected Planning Workbench

**Built by Harsha Vivekananda Muvvala** · [MIT License](LICENSE)

An AI-assisted sales forecasting and planning application that combines the planning discipline of Anaplan, the analytics layer of Power BI, and an agentic close workflow — in one tool, one file, zero build step.

I built this after ten years across R2R, controllership, and FP&A, where I kept seeing the same gap: planning tools calculate, BI tools visualize, but the explanation — the "so what" that goes to the CFO — is still assembled by hand every cycle. This workbench closes that loop. The statistical model does the forecasting; the AI does the explaining; and the AI is only allowed to speak from the live model figures, so commentary can never drift from the data.

## The four layers

### 1. Planning layer (from Anaplan)
- **Driver-based scenarios** — Pessimistic / Base / Optimistic growth drivers per segment; edit any cell and the whole model recalculates live. A probability-weighted expected value collapses the fan into one planning number.
- **Versions** — Budget is a locked snapshot; the Working Forecast recalculates on every edit.
- **Breakback** — edit a month's total and it spreads proportionally down through segments and scenarios, with the override flagged for audit.
- **Rolling re-base** — when actuals land, the forecast re-anchors on the actual, not the stale budget, and every landed month is scored against what the model predicted at the time.

### 2. Analytics layer (from Power BI)
- **Scenario fan** — actuals trajectory with the three cases fanning ahead, plus the EV line.
- **Variance bridge** — a Budget → Forecast waterfall where segment deltas sum exactly to the total.
- **Cross-filtering** — select a segment and every visual and KPI filters to it.
- **KPI cards and conditional formatting** on variance dollars and percentages.

### 3. Agentic workflow layer (the part neither tool has)
When a month's actuals land, an autopilot pipeline runs end to end:
1. **Detects** the new actuals and re-bases the rolling forecast.
2. **Generates commentary** — CFO-ready, following what happened → why → what to change in the model → what constraint to protect.
3. **Notifies the FP&A manager** — drafts a notification email summarizing the close, variance, and re-based outlook, ready to open in your mail client.
4. **Suggests planning actions** — three numbered, imperative moves with figures, each convertible to a task in one click.
5. **Opens a review task** — every close creates an approval item; approve to sign off the re-based forecast, reject to send it back to planning. A notifications feed keeps the full audit trail.

Autopilot can be switched off for a manual cycle.

### 4. Data layer
- **Load your own CSV** — first column is the date, each remaining column becomes a segment. Monthly or daily rows both work (daily rows are summed into months). Growth drivers are seeded from each segment's trailing growth, and a budget snapshots automatically.
- Or load the bundled sample model: 3 segments, 12 months of actuals.

## Design principle

The AI is deliberately **not** the forecaster. Transparent, testable statistics generate the numbers; the AI translates them into commentary, notifications, and actions. That keeps the forecast auditable and the narrative trustworthy — the two things a finance leader actually needs.

## Running it

- **Hosted**: the CI/CD workflow in this repo deploys `index.html` to GitHub Pages on every push to `main`.
- **Local**: open `index.html` in any modern browser. No install, no build — React, Recharts, and Babel load from CDN.
- **AI features**: the commentary, notification, and Q&A features call the Anthropic API and are fully functional when the app runs inside Claude (claude.ai artifacts). In a standalone browser the planning, analytics, and workflow scaffolding all work; the agent steps require an API key.

## Repository structure

```
index.html                    — the complete application (single file)
src/planning-workbench.jsx    — the React component source
.github/workflows/ci-cd.yml   — validate JSX on every push/PR, deploy to Pages on main
LICENSE                       — MIT
```

## How it's built

React single-page application with Recharts for visuals and the Anthropic API (Claude) as the embedded agent. The planning engine — anchoring, compounding drivers, probability weighting, breakback spreading, and holdout accuracy scoring — is implemented from scratch, so every number is traceable to a formula, not a black box.

The methodology draws on my production experience: a daily sales forecasting model I ran for a Fortune 500 US healthcare retailer (day-of-week weighted, 12-week rolling window, 97.4% accuracy across 50 stakeholders) and multi-scenario Anaplan model design from my [connected-planning portfolio work](https://github.com/harshamuvvala18-max) on SEC-filed actuals.

---

*Harsha Vivekananda Muvvala — FP&A | Connected Planning | Anaplan Professional Model Builder | Microsoft PL-300*
