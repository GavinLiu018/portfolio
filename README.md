# Gavin Liu

**Statistics student · Sports analytics · R & Python**

I'm a statistics student at **[UCLA]** (expected graduation **[Spring 2028]**) looking for a
**Summer 2027 internship** in data science, statistical analysis, or sports analytics. I like
turning messy real-world data into models and tools that people can actually use, and I care about
getting the numbers right: validating inputs, testing code, and checking where a metric can mislead.

[LinkedIn]([https://www.linkedin.com/in/gavin-liu-stats/]) · [Email](mailto:[gavin.t.liu@gmail.com]) · [Resume]([[ResumeGavinLiu.pdf](https://github.com/GavinLiu018/portfolio/blob/main/ResumeGavinLiu.pdf)])

---

## Projects

### 🏈 [NFL Player Rankings](https://github.com/GavinLiu018/nfl-player-analysis): configurable scoring model + interactive app

A local app that ranks every NFL player in the 2026 season using a scoring model the user
configures per position. I built it **twice, in R (Shiny) and Python (Streamlit)**, sharing one
config and data layer, with a test that checks both versions give every player the same score.

**What I did**
- **Statistical model:** each metric is converted to a percentile among *qualified* players at that
  position (ties counted as half), or to a z-score passed through the normal CDF. The player's score is
  the weighted average × 100. Users choose metrics, weights (0–10), direction, and qualification rules.
- **Data pipeline:** downloads nightly [nflverse](https://github.com/nflverse) releases (~150 stat
  columns per player) and replaces the cached data only if every row is from the right season and all
  expected columns are present. If a check fails, the old data is kept.
- **Correct aggregation over week ranges:** counting stats are summed, while rate stats (target
  share, air-yards share, PACR, RACR, FG%) are *recomputed* from team totals instead of averaged, and
  CPOE is weighted by pass attempts.
- **Safe custom metrics:** users can define metrics like `(rushing_yards + receiving_yards) / games`.
  The parser accepts only arithmetic and column names, so arbitrary code can't run.
- **Engineering:** unit tests in `testthat` and `pytest`, an R-vs-Python parity check, and one-click
  launchers for Windows and macOS.

`R` `Shiny` `Python` `Streamlit` `pandas` `testthat` `pytest` `YAML`

---

### 📈 [NFL Contract-Year Performance & Compensation](https://github.com/GavinLiu018/nfl-contract-year): exploratory analysis (2015–2023)

Do NFL players really play better in the final year of their contract, and does contract-year
performance predict the guaranteed money on their next deal?

**What I did**
- **Data engineering:** joined OverTheCap contract records to weekly game logs for **1,249 offensive
  players (50,265 player-games)**, kept only games inside each contract's active seasons, and
  flagged contract years (`season == season_end`).
- **Feature engineering:** total EPA (passing + rushing + receiving), completion %, yards per carry,
  and catch rate per game.
- **Modeling:** OLS regressions of next-contract guaranteed money on contract-year EPA, fit separately
  for QBs, WRs, and RBs.

**Key findings**
- **No contract-year bump for RBs.** Average EPA per game is about the same in contract and non-contract
  years. RB EPA is negative on average, yet RBs are the 4th highest-paid position by APY, which suggests
  EPA undervalues their steady, drive-sustaining gains (≈4.0 yards per carry).
- **WRs: averages hide who is in the sample.** Across all receivers, yards and receptions per game drop in
  contract years, mostly because of depth receivers losing targets. For high-volume WRs (65+ yards per
  game) the drop disappears.
- **The market rewards QB efficiency most.** Next-contract guarantees rise most steeply with contract-year
  EPA for QBs (slope 1.60), then WRs (1.09), then RBs (0.86).

`R` `R Markdown` `dplyr` `ggplot2` `nflfastR` `nflreadr` `Linear regression`

---

## Skills

| Area | Tools & methods |
|---|---|
| **Languages** | R, Java |
| **Statistics** | Linear regression (OLS), exploratory data analysis, percentile & z-score normalization, weighted composite indices |
| **Data** | `dplyr`, `pandas`, data cleaning & joins, feature engineering, data validation |
| **Visualization** | `ggplot2`, Shiny, Streamlit, interactive dashboards |
| **Workflow** | Git/GitHub, R Markdown, unit testing (`testthat`, `pytest`), reproducible pipelines |

## Relevant coursework

*[Probability, Programming with R, Introduction to Data Science, Introduction to Statistical Reasoning, Linear Algebra & Applications, Multivariable Calculus]*

## What I'm working on next

- Adding R², p-values, and controls (age, injury history, cap-adjusted guarantees) to the contract-year regressions
- Extending the contract-year analysis to tight ends and defensive players
- Embedding key figures from both projects directly in their READMEs

---

📫 **Open to Summer 2027 internships.** The best way to reach me is [gavin.t.liu@gmail.com] or
[LinkedIn]([https://www.linkedin.com/in/gavin-liu-stats/]).
