# Facebook Ads Analyst — Claude Code Skill & Agent

A Claude Code skill and agent that analyzes Facebook/Meta Ads reports, finds
performance gaps with explanations and fixes, and builds a campaign strategy.

## What's included

| Path | What it is |
|---|---|
| `.claude/skills/facebook-ads-analyst/SKILL.md` | The skill: 5-step analysis workflow with hard accuracy rules |
| `.claude/skills/facebook-ads-analyst/references/benchmarks.md` | Default benchmarks and health heuristics |
| `.claude/skills/facebook-ads-analyst/references/diagnostics.md` | Top-down funnel gap-diagnosis decision tree |
| `.claude/skills/facebook-ads-analyst/references/strategy-playbook.md` | Budget, kill/fix/scale, creative testing, and 30-day plan rules |
| `.claude/agents/fb-ads-analyst.md` | Subagent that runs the whole pipeline end-to-end |

## How to use

1. Export a report from Meta Ads Manager (CSV or XLSX). Include at minimum:
   spend, impressions, link clicks, and your result column (purchases/leads),
   plus landing page views, frequency, and video metrics if available.
   Campaign + ad set + ad level exports give the deepest analysis.
2. Drop the file into this repo (or paste the table) in a Claude Code session.
3. Run the skill:

   ```
   /facebook-ads-analyst analyze report.csv — my target CPA is $25
   ```

   Or just ask naturally ("analyze my Facebook ads report and find the gaps") —
   the skill auto-triggers on ad-report tasks. For long analyses you can also
   delegate: "use the fb-ads-analyst agent on report.csv".

4. You get a written report in `reports/` covering:
   - Full metric funnel (CPM → CTR → CPC → connect rate → CVR → CPA/ROAS)
   - Ranked gaps, each with what/why/root-cause/fix and the money impact
   - Budget reallocation table and kill / fix / scale list
   - 30-day week-by-week action plan and a measurement plan

## Accuracy guarantees built into the skill

- All metrics recomputed from raw columns with Python — no mental math, no
  trusting exported ratio columns.
- Input validation and tracking-integrity checks run before any analysis;
  broken pixel/CAPI data halts the performance analysis instead of producing
  garbage conclusions.
- No fabricated numbers or benchmarks; when a default benchmark is used instead
  of your target, the report says so.
- Low-sample results (< 20 conversions) are labeled directional, and
  learning-phase ad sets are never judged as failures prematurely.
