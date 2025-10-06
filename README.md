# Quant systems engineering

I build small, reliable systems for **signals → decisions → execution**. Current focus: clock-aligned schedulers, bounded randomness, regime/human awareness, and measured latency — plus the telemetry to prove it.

Current focus: cadence control (TWAP-like scheduling with bounded jitter), mean-reverting drift modules, and latency measurement. Up next: a small, testable stack — multi-horizon signals, regime classification, cost-aware bet sizing, and execution with kill-switches.

**Background:** ~5 years sell-side investment banking — bringing execution discipline, controls, and model hygiene, while avoiding process bloat. **Automation-first:** code over manual spreadsheets; small, reproducible pipelines with clear interfaces.

---

## What I’m building toward

- **Upstream signal layer.** Ingest market/alt data and construct multi-horizon predictive curves. Blend alphas such as trend, carry, lead–lag, and cross-sectional relative value into a unified view; compare signals across assets/regions and time horizons.
- **Regime awareness & noise reduction.** Segment history into policy/volatility regimes to avoid overfit; include alternative data thoughtfully given short histories and duplication with price moves.
- **Sentiment & anomaly scanning.** Track language features (frequency, rate-of-change), news/IR streams, and price/volume anomalies; differentiate genuine signals from narrative noise.
- **Downstream strategy layer.** Turn prediction curves into positions with **transaction-cost awareness** across horizons; size with fractional-Kelly-style logic; monitor realised risk/Sharpe.
- **Scanning cadence & data plumbing.** Continuous/live lists for candidates, periodic rescans, and an incremental database so we update deltas rather than refetching history.

---

## Recent & representative work

- **Clock-aligned scheduler with bounded randomness.** A tight execution loop that keeps cadence on a wall-clock with soft-clamped jitter, plus non-blocking movement/drift so animation never steals time from the schedule.
- **Mean-reverting motion modules.** Human-like “wander → recenter” corrections implemented as short Bézier segments with tapered noise — useful patterns for any system that needs stochastic drift with a target.

> Small, focused proofs I’ll reuse in future projects: cadence control, bounded randomness, regime-aware knobs, and tidy termination (e.g., global kill-switches) scale nicely.

---

## Roadmap (next experiments)

### Signals & features
- Multi-horizon curves from trend/carry/lead–lag/relative value; cross-asset comparators  
- Regime classifier (policy/vol/market states) + regime-specific hyper-parameters  
- Sentiment features: frequency & rate-of-change, news/IR filters; anomaly detectors for price/volume  
- Careful inclusion of short-history alt-data with guardrails

### Strategy & sizing
- Transaction-cost modelling across horizons; **fractional Kelly** bet sizing with caps; realised-risk targeting  
- Telemetry: inter-trade interval histograms/QQ plots; latency budgets; regime-split performance

### Infra & orchestration
- Live candidate lists with decay rules; incremental database updates; configurable scan cadence  
- Clean interfaces so upstream/downstream pieces can be A/B tested and swapped

---

## How I like to work

- **Clock first.** Schedule off a single timebase; work in time-slices to keep the loop honest  
- **Bounded randomness.** Be stochastic, but clamp the tails; predictable in aggregate  
- **Regime-aware.** Don’t let one era dominate priors; evaluate by state  
- **Human-aware.** *History rhymes because psychology repeats.* Markets are aggregates of emotional agents. Herding, loss aversion and reflexivity persist; models account for **overshooting in rallies** and **capitulation in selloffs**  
- **Fail fast, fail safe.** Kill-switches, corner failsafes, and non-blocking loops  
- **Tight surfaces.** Small APIs; a few parameters that actually move the needle

---

## Tech stack

Python; small scientific stack (NumPy) and focused utilities for scanning, scheduling, and lightweight plotting/telemetry. Comfortable on Windows; cross-platform when it makes sense.

---

## Get in touch

Issues and discussions welcome. If you’re building something adjacent (execution, scheduling, regime detection, anomaly scanning), I’m up for comparing notes.

<sub>Unless otherwise noted, code is MIT-licensed.</sub>
