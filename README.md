# Geopol Forecasts Index

Index of prediction runs produced by [Geopol Forecaster](https://github.com/danielrosehill/Geopol-Forecaster), a two-stage geopolitical forecasting pipeline combining [Snowglobe](https://github.com/IQTLabs/snowglobe)-style actor simulation with [LLM Council](https://github.com/karpathy/llm-council)-style multi-perspective analytical review.

Each run is seeded with live news data and produces probabilistic forecasts with credible intervals across multiple time horizons.

Accuracy analysis will be added as prediction windows close and ground truth becomes available.

---

## Prediction Runs

| # | Date | Topic | Actors | Lenses | Model | Open-Sourced Report | Key Finding |
|---|------|-------|--------|--------|-------|-------------------|-------------|
| 2 | 09/04/2026 | Iran-Israel-US ceasefire durability | 38 | 6 | Claude Sonnet 4.5 | [Iran-Israel-Ceasefire-Prediction-090426](https://github.com/danielrosehill/Iran-Israel-Ceasefire-Prediction-090426) | 22% chance ceasefire holds at +72h (simulation: 28% -- 6-point convergence between independent stages) |
| 1 | 24/03/2026 | Iran-Israel-US conflict trajectory (Day 25) | -- | 6 | -- | [Iran-Israel-Conflict-Trajectory-240326](https://github.com/danielrosehill/Iran-Israel-Conflict-Trajectory-240326) | 5/5 high-confidence predictions validated; ceasefire (April 8) was not anticipated |

---

## Accuracy Tracking

| Run | Window | Prediction | Actual Outcome | Accuracy | Notes |
|-----|--------|------------|----------------|----------|-------|
| 1 | 24h-1wk | Israeli operations continue at full intensity | IDF continued strikes through March and into April | Correct | 6/6 lenses agreed |
| 1 | 24h-1wk | Iranian proxy retaliations continue | Hezbollah maintained 55+ attacks/day | Correct | 5/6 lenses agreed |
| 1 | 1mo | Iranian ballistic missile capabilities degraded 50%+ | Coalition struck ~330/470 launchers (70%) | Correct | 5/6 lenses agreed |
| 1 | 1mo | IDF maintains/extends Lebanon buffer zone to Litani | IDF reached Litani River by March 24 | Correct | 5/6 lenses agreed |
| 1 | 1wk | March 27 deadline fails (no deal reached) | No deal; war continued until April 8 ceasefire | Correct | 5/6 lenses agreed |
| 1 | 1mo | No ceasefire holds before March 27 | Ceasefire came April 8 (after deadline) -- not anticipated | Partially correct | Timeframe was right; ceasefire ultimately happened later |
| 2 | +72h | 22% chance ceasefire holds at 72h | *Window still open at time of indexing* | TBD | Simulation gave 28% |

---

## Pipeline Overview

```
Stage 0: Gather fresh data (Tavily news search + ISW/RSS feeds)
         Freeze into identical world state for all participants
              |
Stage A: Snowglobe-style actor simulation
         N actors x T timesteps, referee-narrated world state
         Each actor commits privately and independently
              |
Stage B: LLM Council 6-lens analytical panel
         Independent answers --> blind peer review --> chairman synthesis
         Sees: prompt + fresh data + Stage A simulation summary
              |
Output:  Chairman report, per-lens answers, cross-reviews,
         simulation transcript, executive PDF, archival PDF
```

### What makes the convergence interesting

Stages A and B are **completely independent analytical processes**:
- Stage A simulates actors making decisions in a game-theoretic loop -- it produces emergent outcomes from 38 agents reasoning from their own persona
- Stage B runs six analytical lenses through structured deliberation -- it produces calibrated probabilities from expert-style reasoning

Neither stage has access to the other's reasoning during execution. When they converge on similar probability estimates (as in the 09/04/2026 run where the simulation gave 28% and the council gave 22% for the 72-hour window), it suggests the pipeline is surfacing genuine signal rather than averaging noise.

---

## Related Repositories

- **[Geopol-Forecaster](https://github.com/danielrosehill/Geopol-Forecaster)** -- the pipeline source code
- **[Geopol-Forecaster-Planning](https://github.com/danielrosehill/Geopol-Forecaster-Planning)** -- design docs and planning
- **[AI-Geopol-Projects](https://github.com/danielrosehill/AI-Geopol-Projects)** -- curated list of AI geopolitical simulation projects
- **[Geopolitical-And-OSINT-Index](https://github.com/danielrosehill/Geopolitical-And-OSINT-Index)** -- broader OSINT and geopolitical analysis index

---

## Author

Daniel Rosehill
[danielrosehill.com](https://danielrosehill.com)
