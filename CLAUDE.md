# CLAUDE.md — Geopol Forecasts Index

Index of prediction runs from [Geopol Forecaster](https://github.com/danielrosehill/Geopol-Forecaster). This repo tracks runs, links to individual experiment repos, and scores prediction accuracy.

## Accuracy Rubric

All predictions are graded on a standard 4-point scale:

| Grade | Score | Criteria |
|-------|-------|----------|
| **Correct** | 1.0 | Core prediction matched reality in direction and approximate magnitude/timing |
| **Largely Correct** | 0.75 | Direction right, magnitude or timing off by a modest margin |
| **Partially Correct** | 0.5 | General direction right but significantly off on timing, magnitude, or mechanism |
| **Incorrect** | 0.0 | Prediction contradicted by what actually happened |
| **Not Yet Testable** | — | Window still open or insufficient data |

Scoring rules:
- Score **direction** first, then adjust for timing/magnitude
- >2x timing error drops a Correct to Largely Correct or below
- Binary predictions ("X won't happen") are scored on the stated claim, not the probability
- Wire services (Reuters, AP) take precedence over opinion sources

## Experiment Repo Convention

Each individual experiment repo should include a **Prediction Tracker** header block linking back to this index:

```markdown
> **Prediction Tracker**: This run is tracked in the [Geopol Forecasts Index](https://github.com/danielrosehill/Geopol-Forecasts-Index).
> Accuracy is assessed using the standard rubric as prediction windows close.
```

## Validation Workflow

Use `/validate-predictions` to run Tavily searches against open predictions and update the accuracy table.
