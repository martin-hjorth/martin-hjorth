# Quant systems engineering

I build small, reliable systems for **signals → decisions → execution** — with telemetry to prove it.

- **Current focus:** cadence control (TWAP-like scheduling with bounded jitter), mean-reverting drift modules, latency measurement.  
- **Next up:** small, testable stack — multi-horizon signals, regime classification, cost-aware bet sizing, execution with kill-switches.

<sub>Guard the signal • Reduce the noise</sub>

---

**Recent and representative work**

- **Clock-aligned scheduler with bounded randomness.** Stochastic control loop: wall-clock cadence with soft-clamped (bounded-tail) jitter, time-sliced so movement/drift never steals time from the schedule.
- **Mean-reverting motion modules.** Human-like “wander → recentre” using short quadratic Bézier segments with tapered Gaussian noise; occasional biased drift then correction toward the centre.

> Small, focused proofs I’ll reuse in future projects: cadence control, bounded randomness, regime-aware knobs, and tidy termination (e.g., global kill-switches) scale nicely.

---

**How I like to work**

- **Clock first.** Schedule off a single timebase; work in time-slices to keep the loop honest.
- **Bounded randomness.** Be stochastic, but clamp the tails; predictable in aggregate.
- **Regime-aware.** Don’t let one era dominate priors; evaluate by state.
- **Human-aware.** *History rhymes because psychology repeats.* Markets are aggregates of emotional agents. Herding, loss aversion and reflexivity persist; models account for **overshooting in rallies** and **capitulation in sell-offs**.
- **Fail fast, fail safe.** Kill-switches, corner failsafes, and non-blocking loops.
- **Tight surfaces.** Small APIs; a few parameters that actually move the needle.

---

**Background**

- **Sell-side investment banking (~5 years):** execution discipline, controls, and model hygiene; keep processes lean. **Automation-first:** code over spreadsheets; small, reproducible pipelines with clear interfaces.
- **Fintech data/automation (~1 year):** reconciliation discipline, schema-aware ingestion, and pattern recognition distilled into rules to automate accounting feeds; minimise manual exceptions. **Automation-first:** deterministic, rules-driven pipelines (SQL + light Python), auditable and low-touch.

---

<details>
  <summary><b>What I’m building toward</b> (expand)</summary>

- **Upstream signal layer**
  - Ingest market/alt data and construct multi-horizon predictive curves.
  - Blend alphas such as trend, carry, lead–lag, and cross-sectional relative value into a unified view.
  - Compare signals across assets/regions and time horizons.

- **Regime awareness and noise reduction**
  - Segment history into policy/volatility regimes to avoid overfit.
  - Include alternative data thoughtfully, given short histories and duplication with price moves.

- **Sentiment and anomaly scanning**
  - Track language features (frequency, rate-of-change), news/IR streams, and price/volume anomalies.
  - Differentiate genuine signals from narrative noise.

- **Downstream strategy layer**
  - Turn prediction curves into positions with **transaction-cost awareness** across horizons.
  - Size with fractional Kelly; monitor realised risk/Sharpe.

- **Scanning cadence and data plumbing**
  - Maintain continuous/live lists for candidates with periodic rescans.
  - Use incremental database updates (deltas, not refetch).

</details>

---

<details>
  <summary><b>Roadmap (next experiments)</b> (expand)</summary>

- **Signals and features**
  - Multi-horizon curves from trend/carry/lead–lag/relative value; cross-asset comparators.
  - Regime classifier (policy/vol/market states) with regime-specific hyper-parameters.
  - Sentiment features: frequency and rate-of-change, news/IR filters; anomaly detectors for price/volume.
  - Careful inclusion of short-history alt-data with guardrails.

- **Strategy and sizing**
  - Transaction-cost modelling across horizons; **fractional Kelly** bet sizing with caps; realised-risk targeting.
  - Telemetry: inter-trade interval histograms/QQ plots; latency budgets; regime-split performance.

- **Infra and orchestration**
  - Live candidate lists with decay rules; incremental database updates; configurable scan cadence.
  - Clean interfaces so upstream/downstream pieces can be A/B tested and swapped.

</details>

---

<details>
  <summary><b>Research and modelling principles</b> (expand)</summary>

- **Ablate by default**
  - Keep 2–3 strong baselines; add one idea at a time.
  - Keep it only if it wins out-of-sample and in an ablation table.

- **Evaluate by regime**
  - Tag data by volatility/policy/market states.
  - Report Sharpe, hit rate, turnover, drawdown per state.

- **Guard against leakage**
  - Past-only features; event-time alignment; purged CV with embargo.
  - Reindex joins; forbid forward-fills across the split.

- **Parsimony first**
  - Start with linear / Elastic Net / GBM; regularise and use monotonic constraints.
  - Escalate model complexity only for stable OOS gains.

- **Prioritise robustness**
  - Sensitivity sweeps on windows/params; bootstrap/Monte-Carlo “wobble”.
  - Aim for graceful degradation rather than peak fits.

- **Cost-aware from day one**
  - Include slippage/fees and turnover penalties in objectives.
  - Report P&L with best/typical/worst cost scenarios.

- **Sizing with brakes**
  - Fractional Kelly with caps; volatility targeting.
  - Drawdown de-risking and circuit-breakers.

- **Make it observable**
  - Log predictions, decisions, orders/fills; calibration and residual plots.
  - Track inter-event intervals and latency p50/p95/p99; alert on drift/data gaps.

- **Reproducible runs**
  - Pin the environment and seeds; compute a config hash per run.
  - Store artefacts keyed by run ID.

</details>

---

**Tech stack**

- **Core:** Python (3.11+), NumPy, pandas, statsmodels.
- **Modelling:** scikit-learn, LightGBM/XGBoost (only if they win OOS).
- **Data layer:** Parquet/Arrow, DuckDB (local analytics), yfinance/ccxt or custom loaders.
- **Scheduling and ops:** schedule (lightweight) or APScheduler; structured logging (Rich/Loguru); CLI scripts.
- **Testing and quality:** pytest, coverage, Ruff/Black, pre-commit.
- **Packaging and env:** uv or Poetry; pinned lockfiles; `.env` via pydantic-settings.
- **Viz/telemetry:** matplotlib/plotly; simple dashboards/tables for calibration, residuals, latency.
- **OS:** Windows primary; cross-platform when it makes sense.

---

**Get in touch**

Issues and discussions welcome. If you’re building something adjacent (execution, scheduling, regime detection, anomaly scanning), I’m up for comparing notes.

<sub>Unless otherwise noted, code is MIT-licensed.</sub>
