# Cookie Cats A/B test

Does moving the first progression gate in a mobile game from level 30 to level
40 keep players around longer? Analysis of 90,189 players, run twice — once with
frequentist hypothesis tests and once with a Bayesian model — because the two
answer subtly different questions.

**Conclusion: no. Ship gate_30.** Moving the gate to level 40 does not improve
retention and probably reduces it.

## Results

| Test | Result |
|---|---|
| Game rounds (Mann-Whitney U) | Statistically significant, but Cliff's Delta is negligible |
| 1-day retention (Chi-square) | Not significant; Cramér's V shows weak association |
| 7-day retention (Chi-square) | Not significant |
| **1-day retention, P(gate_40 > gate_30)** | **3.66%** |
| **7-day retention, P(gate_40 > gate_30)** | **0.06%** |

The game-rounds result is the interesting one, and the reason both methods are
here. With 90k players the Mann-Whitney test detects a difference that is real
but far too small to act on — significance without practical importance. The
Bayesian view states the thing a product decision actually needs: the
probability that the new gate is better at all, which is 3.66% at one day and
essentially zero at seven.

## What it does

- Cleans the data and examines the heavily skewed, non-normal round counts
- Tries Winsorization and log transforms; neither achieves normality, which is
  what motivates the non-parametric tests
- Runs Mann-Whitney U with Cliff's Delta for effect size, and Chi-square with
  Cramér's V for the retention flags
- Models retention as Beta-Binomial with an uninformative prior and draws
  100,000 posterior samples per group

## Quick start

```bash
pip install -r requirements.txt
jupyter notebook cookie_cats_ab_test.ipynb
```

The notebook renders with its output on GitHub, so you can read the whole
analysis without running anything.

| Path | What it is |
|---|---|
| `cookie_cats_ab_test.ipynb` | the analysis |
| `cookie_cats.csv` | 90,189 players, one row each |

## License

MIT — see [LICENSE](LICENSE).
