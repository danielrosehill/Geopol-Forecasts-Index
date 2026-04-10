---
name: validate-predictions
description: Use Tavily search to check Geopol Forecaster predictions against real-world outcomes and score them using the standard accuracy rubric
user_invocable: true
---

# Validate Predictions

Search for real-world outcomes to assess Geopol Forecaster predictions against reality.

## Steps

1. **Read the index** — Read `README.md` to find all predictions in the Accuracy Tracking table, paying attention to any marked `TBD` or with open windows.

2. **Identify testable predictions** — A prediction is testable if its time window has closed (compare the run date + window against today's date). Skip any whose window is still open.

3. **Search for ground truth** — For each testable prediction, use `mcp__jungle-shared__tavily__tavily_search` with:
   - A focused query derived from the prediction (e.g. `"Iran Israel ceasefire April 2026 status"`)
   - `search_depth: "advanced"`
   - `max_results: 10`
   - `topic: "general"`
   - Prefer news sources: Reuters, AP, Times of Israel, BBC, Al Jazeera

4. **Score each prediction** using the standard rubric:

   | Grade | Score | Criteria |
   |-------|-------|----------|
   | **Correct** | 1.0 | Core prediction matched reality in both direction and approximate magnitude/timing |
   | **Largely Correct** | 0.75 | Direction right, magnitude or timing off by a modest margin |
   | **Partially Correct** | 0.5 | Got the general direction but missed significantly on timing, magnitude, or mechanism |
   | **Incorrect** | 0.0 | Prediction contradicted by what actually happened |
   | **Not Yet Testable** | — | Window still open or insufficient public reporting to assess |

5. **Update the Accuracy Tracking table** in `README.md`:
   - Fill in the `Actual Outcome` column with a concise (1-sentence) summary of what happened, citing the strongest source
   - Set `Accuracy` to the rubric grade
   - Add brief `Notes` explaining the score
   - For any prediction whose window is still open, leave as `TBD`

6. **Compute a run-level score** — For each run that has at least one graded prediction, compute:
   - `Run Score = mean(scored predictions)` (excluding Not Yet Testable)
   - `N graded / N total` predictions assessed
   - Append this as a summary row or note below the table

7. **Report** — Print a short summary of what changed: which predictions were newly graded, what the scores were, and any notable findings from the search.

## Rubric Design Notes

- Score **direction** first (did the predicted thing happen or not?), then adjust for **timing** and **magnitude**.
- A prediction that got the direction right but was off by >2x on timing drops from Correct to Largely Correct or Partially Correct.
- A prediction that the model assessed as unlikely (<25%) which then happened is scored on what the prediction *said would happen*, not the probability — i.e., if the model said "ceasefire unlikely" and a ceasefire happened, that's Incorrect on the binary prediction even if the low confidence was well-calibrated.
- When sources conflict, prefer wire services (Reuters, AP) over opinion pieces.
