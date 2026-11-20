# NFL Contract Year Performance & Compensation Analysis (2015–2023)

An exploratory data analysis (EDA) project investigating the "Contract Year Phenomenon" in the National Football League (NFL) and how on-field efficiency translates into guaranteed compensation in subsequent contracts.

**Author:** Gavin Liu  
**Tech Stack:** R (`dplyr`, `ggplot2`, `nflfastR`, `nflreadr`)

---

## 📌 Project Overview

In professional sports, a common narrative suggests that athletes elevate their performance during the final year of their contracts to maximize their free-agent market value. Using historical NFL contract data and weekly player performance metrics from **2015 to 2023**, this project explores:
1. Whether offensive skill players (RBs and WRs) actually perform better during their contract years.
2. Why Expected Points Added (EPA) can be misleading when evaluating Running Backs compared to traditional efficiency metrics.
3. How strongly a player's contract-year EPA correlates with the guaranteed money they receive on their next deal across different positions (QBs, RBs, WRs).

---

## 📊 Data Sources & Methodology

Data was programmatically sourced via the `nflverse` ecosystem (`nflreadr` & `nflfastR`), combining historical OverTheCap contract records with weekly offensive player statistics.

### Data Engineering Pipeline:
* **Temporal Alignment:** Joined contract records (`gsis_id`) with weekly performance logs (`player_id`) across 1,249 unique offensive players, strictly filtering game logs to fall within each contract's active start and end seasons (`2015–2023`).
* **Contract Year Flagging:** Created a boolean indicator (`contract_year`) identifying whether a given season represented the final year of a player's active contract (`season == season_end`).
* **Feature Engineering:** Computed custom per-game efficiency metrics across 50,265 player-game observations:
  * `total_epa`: Combined passing, rushing, and receiving Expected Points Added.
  * `completion_percent`: Passing completions divided by attempts.
  * `yards_per_carry`: Rushing yards divided by carries.
  * `catch_rate`: Receptions divided by targets.

---

## 🔍 Key Findings

### 1. The Running Back EPA Paradox
* **No Contract Year Bump:** Running backs show virtually identical average EPA per game in contract years versus non-contract years (hovering around `-0.65` EPA/game).
* **EPA vs. Yards Per Carry:** Despite negative average EPA (which heavily favors explosive passing plays over short, consistent gains), RBs rank as the **4th highest-paid position** by Average Per Year (APY). Evaluating RBs via **Yards Per Carry (~4.0 YPC)** reveals steady, positive drive-sustaining value that EPA alone obscures.

### 2. Star vs. Replacement-Level Wide Receivers
* **The Overall Dip:** Across all wide receivers, average receiving yards per game (`~41` vs. `~28` yds) and receptions per game (`~3.2` vs. `~2.3`) actually *drop* during contract years—largely driven by depth/replacement-level receivers losing target share or roster spots.
* **Elite Consistency:** When isolating high-volume receivers averaging **65+ receiving yards per game** (~1,100+ yards/season), the contract-year drop disappears entirely, showing consistent quarterback target volume regardless of contract status.

### 3. Contract Year EPA vs. Next Contract Guaranteed Money
Using ordinary least squares (OLS) linear regression (`guaranteed_next ~ contract_year_epa`), positional market sensitivity to contract-year efficiency varies substantially:
* **Quarterbacks (Slope: `1.60`):** Highest financial return per unit of contract-year EPA, reflecting the premium placed on QB efficiency in free agency and extensions.
* **Wide Receivers (Slope: `1.09`):** Strong positive relationship between contract-year efficiency and future guaranteed money.
* **Running Backs (Slope: `0.86`):** Lowest sensitivity to contract-year EPA, aligning with broader NFL positional devaluation trends for aging running backs.

---

## 📁 Repository Structure

```text
├── stat15_eda.Rmd       # Main R Markdown file containing data cleaning, feature engineering, & visualizations
├── stat15_eda.pdf       # Knitted PDF report with embedded plots and analytical commentary
└── README.md            # Project documentation
```

---

## 🚀 How to Run Locally

1. **Clone the repository:**
   ```bash
   git clone https://github.com/yourusername/nfl-contract-year-eda.git
   cd nfl-contract-year-eda
   ```
2. **Install required R packages:**
   ```r
   install.packages(c("nflfastR", "nflreadr", "dplyr", "ggplot2", "rmarkdown"))
   ```
3. **Knit the R Markdown document:**
   Open `stat15_eda.Rmd` in RStudio and click **Knit**, or run:
   ```r
   rmarkdown::render("stat15_eda.Rmd")
   ```

---

## 🔮 Future Improvements
* Incorporate $R^2$, p-values, and multivariate controls (e.g., player age, injury history, salary cap inflation via `inflated_guaranteed`) into the regression models.
* Expand positional analysis to include Tight Ends (TE) and defensive players.
* Export key `ggplot2` figures into an `/images` folder to embed directly in this README.