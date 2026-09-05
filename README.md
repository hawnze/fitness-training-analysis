# fitness-training-analysis
Personal Fitness Data Analysis

**A personal data science project analyzing 12+ months of gym workout logs to uncover patterns in training volume, strength, and bodyweight changes during Bulk and Cut phases.**

**Author:** Hans Dano  
**Tools:** R (tidyverse, ggplot2, dplyr, tidyr, lubridate), R Markdown, Linear Regression  
**Link:** [GitHub Repository](https://github.com/hawnze/fitness-training-analysis)

---

## Overview

This project applies the full data science pipeline—from data cleaning and feature engineering to statistical modeling and visualization—to a real-world dataset of personal workout logs. 

Using over 1,000 rows of tracked gym sessions, I explored the relationships between training variables and physiological outcomes, while navigating common real-world data challenges like missing values, inconsistent exercise names, and small sample sizes.

---

## Key Questions Investigated

1. **Cut Phase:** Does weekly training volume predict weekly weight loss?
2. **Bulk Phase:** Does having more rest days between Push sessions lead to higher performance (1RM) on Incline Dumbbell Press?
3. **Descriptive:** How does training volume distribution differ between muscle groups (Legs, Push, Pull), and how did these patterns evolve over time?

---

## Data & Features

- **Raw Data:** 1,000+ rows of personal gym logs (2025–2026), tracking exercise, weight lifted, reps, sets, and bodyweight (Cut phase only).
- **Feature Engineering:**
  - **Volume:** `weight × reps` (per set, daily, weekly, and monthly aggregates).
  - **1RM (One-Rep Max):** Estimated using the Epley formula: `weight × (1 + reps/30)`.
  - **Rest Days:** Calculated as the number of days between Push-sessions (with gaps > 7 days treated as missing data to prevent logging gaps from skewing results).
  - **Weight Change:** Weekly bodyweight difference using `lag()`.

---

## Key Findings

- **Weekly Volume vs. Weight Loss (Cut):** Linear regression showed a weak negative trend (slope = -0.000015 per lb of volume), but the result was not statistically significant (p = 0.392, Adj. R² = -0.018). This suggests that weekly volume did not significantly predict weight loss, likely due to the small sample size (n = 12 weeks) and the dominance of dietary factors in weekly weight fluctuations.

- **Rest Days vs. Incline Press Strength (Bulk):** The model showed a positive trend—each additional rest day was associated with a +1.69 lb increase in estimated 1RM—but this was not statistically significant (p = 0.074, Adj. R² = 0.144, n = 17 sessions). While suggestive, the small sample indicates that more data is needed to draw definitive conclusions.

- **Descriptive Training Patterns:** 
  - Legs had the highest **total volume** despite having the fewest sets (due to heavier loads like Hack Squats).
  - Push exercises had the highest **total number of sets**, reflecting my preference for upper body training.
  - Training volume naturally tapered off in the weeks leading into the Cut phase, aligning with a transition period.

---


Link to your GitHub: Since you have other projects, you can mention or link to your main GitHub profile: https://github.com/hawnze.
