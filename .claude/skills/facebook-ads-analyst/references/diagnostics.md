# Gap diagnosis decision tree

Work top-down through the funnel. A downstream metric (CPA/ROAS) is never the root
cause — it's the symptom. Find the FIRST broken stage; fixing upstream usually
moves everything below it.

## Stage 0 — Tracking integrity (check before anything else)

Symptoms: zero/near-zero conversions despite healthy clicks; conversions in
Ads Manager wildly below platform/backend numbers; sudden cliff in results on a
specific date.

Causes & checks:
- Pixel or CAPI broken / event mismatch → check Events Manager event match quality,
  test events tool.
- Wrong optimization event selected on the ad set.
- Attribution window changed or iOS-heavy audience underreporting.

Fix: repair tracking first. **Do not analyze performance on broken data** — state
this and stop the performance section until confirmed.

## Stage 1 — Delivery cost (CPM high or rising)

Symptoms: CPM well above account history or rising > 20% week-over-week.

Causes (in likelihood order):
1. Audience too narrow / heavy overlap between ad sets → broaden, consolidate, or
   use Advantage+ audience.
2. Low ad quality ranking / negative feedback → check ad relevance diagnostics;
   refresh creative.
3. Frequency too high (auction fatigue) → new creative or expanded audience.
4. Seasonal auction pressure (Q4, sales events) → expected; judge ROAS not CPM.

## Stage 2 — Ad engagement (CTR low, or hook/hold rates low)

Symptoms: link CTR < 0.7%, hook rate < 20%, CTR declining while frequency rises.

Causes:
1. Creative fatigue (CTR declined over time on same creative) → new angles, not
   just new variations of the same angle.
2. Creative–audience mismatch (CTR low from day 1) → message doesn't speak to this
   audience; test different hooks/value props.
3. Weak hook (good CTR-all but low link CTR, or low hook rate) → first 3 seconds
   and primary text need rework.

Quantify the gap: CPC = CPM / (1000 × CTR), so CTR moving 0.7% → 1.2% cuts CPC
~42% at constant CPM. Show this math.

## Stage 3 — Click-to-land (connect rate low)

Symptoms: landing page views / link clicks < 70%.

Causes: slow page load (esp. mobile), redirects, broken deep links, interstitials.
Fix: page speed audit, remove redirects. This is the cheapest fix in the whole
funnel — pure waste recovery.

## Stage 4 — Conversion (CVR low while CTR is healthy)

Symptoms: traffic is fine, conversions aren't.

Causes:
1. Offer/price vs. expectations set by the ad (message mismatch) → align ad promise
   with landing page; check scroll/bounce if analytics available.
2. Landing page friction (forms, checkout steps, trust signals, mobile UX).
3. Wrong traffic (broad/low-intent audience with high CTR but no intent —
   clickbait-y creative) → check CTR-all vs link-CTR ratio; engagement bait inflates
   the former.
4. Optimization event too shallow (optimizing for ATC when you want purchases).

## Stage 5 — Economics (CPA above target / ROAS below breakeven with healthy funnel)

If every stage above is at benchmark and CPA still misses target, the gap is
structural: AOV too low (bundles, upsells), margin too thin, or LTV not factored.
Recommend business-level fixes honestly instead of pretending an ads tweak will
close it.

## Cross-cutting patterns

- **Fatigue signature**: frequency ↑ + CTR ↓ + CPA ↑ over consecutive weeks → 
  creative refresh cadence gap. Recommend a standing test pipeline (see playbook).
- **Concentration risk**: one ad/ad set carries > 60% of results → flag fragility;
  build backups before it fatigues.
- **Zombie spend**: entities spending with 0 results past 2–3× target CPA → kill list.
- **Premature kills**: entities paused historically before exiting learning → note
  as a process gap.
- **Audience overlap**: many small ad sets in one campaign, each stuck in learning
  → consolidation gap; fewer ad sets, bigger budgets each.
