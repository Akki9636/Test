# Facebook Ads Analyst — Claude Code Plugin

A Claude Code plugin that analyzes Facebook/Meta Ads reports, finds performance
gaps with explanations and fixes, and builds a campaign strategy. This repo is
both the plugin and its own marketplace, so it installs directly from GitHub.

## Install

Inside any Claude Code session:

```
/plugin marketplace add Akki9636/Test
/plugin install facebook-ads-analyst@akki-ads-tools
```

Or from the terminal (non-interactive):

```bash
claude plugin marketplace add Akki9636/Test
claude plugin install facebook-ads-analyst@akki-ads-tools --scope user
```

`--scope user` makes it available in every project on your machine.

To update later: `/plugin marketplace update akki-ads-tools`.

## Use

Export a report from Meta Ads Manager (CSV or XLSX) with at minimum: spend,
impressions, link clicks, and your result column (purchases/leads). Landing page
views, frequency, and video metrics enable deeper analysis.

Then, in any project where the file is reachable:

```
/facebook-ads-analyst:analyze report.csv — my target CPA is ₹500
```

Or just ask naturally ("analyze my Facebook ads report and find the gaps") —
the skill auto-triggers. For long analyses, delegate to the bundled agent:
"use the fb-ads-analyst agent on report.csv".

You get a written report in `reports/` covering:

- Full metric funnel (CPM → CTR → CPC → connect rate → CVR → CPA/ROAS)
- Ranked gaps, each with what/why/root-cause/fix and the money impact
- Budget reallocation table and kill / fix / scale list
- 30-day week-by-week action plan and a measurement plan

## What's in the plugin

| Path | What it is |
|---|---|
| `.claude-plugin/plugin.json` | Plugin manifest |
| `.claude-plugin/marketplace.json` | Marketplace manifest (lets this repo self-distribute) |
| `skills/analyze/SKILL.md` | The skill: 5-step analysis workflow with hard accuracy rules |
| `skills/analyze/references/benchmarks.md` | Default benchmarks and health heuristics |
| `skills/analyze/references/diagnostics.md` | Top-down funnel gap-diagnosis decision tree |
| `skills/analyze/references/strategy-playbook.md` | Budget, kill/fix/scale, creative testing, and 30-day plan rules |
| `agents/fb-ads-analyst.md` | Subagent that runs the whole pipeline end-to-end |

## Accuracy guarantees built into the skill

- All metrics recomputed from raw columns with Python (pandas) — no mental math,
  no trusting exported ratio columns.
- Input validation and tracking-integrity checks run before any analysis; broken
  pixel/CAPI data halts the performance analysis instead of producing garbage
  conclusions.
- No fabricated numbers or benchmarks; when a default benchmark is used instead
  of your target, the report says so.
- Low-sample results (< 20 conversions) are labeled directional, and
  learning-phase ad sets are never judged as failures prematurely.

## Development

Validate after changes:

```bash
claude plugin validate .
```

No `version` field is set in `plugin.json`, so every pushed commit counts as a
new version — installers get updates on `marketplace update` without manual
version bumps.
