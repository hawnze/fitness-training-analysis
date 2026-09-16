# Personal Fitness Data Analysis

A self-directed data analysis project using 12+ months of my own gym training data to explore patterns in training volume, strength, recovery, and bodyweight changes during Bulk and Cut phases.

**Author:** Hans Dano  
**Tools:** R, R Markdown, dplyr, ggplot2, tidyr, lubridate, stringr, Linear Regression

---

## Overview

This project was created as a way for me to apply and further develop my R and statistical analysis skills using a dataset that I personally collected.

The dataset contains over 1,000 exercise-set records from my workouts during 2025–2026, including information such as exercise name, muscle group, weight lifted, repetitions, sets, training phase, and bodyweight.

Because the data came from my own workout logs, it also included many of the problems that appear in real-world datasets, including missing values, inconsistent exercise names, incomplete logging periods, and small sample sizes.

The project follows a general data analysis workflow:

1. Data exploration
2. Data cleaning
3. Feature engineering
4. Data aggregation
5. Visualization
6. Regression analysis
7. Interpretation of results

I intentionally kept detailed comments and intermediate steps in the R Markdown file because this was also a learning project and documents how I worked through problems during the analysis.

---

## Questions Investigated

### 1. Cut Phase

**Does weekly training volume have a relationship with weekly bodyweight change during my Cut?**

The goal was to explore whether weeks with higher recorded training volume were associated with greater changes in bodyweight.

---

### 2. Bulk Phase

**Was having more rest between Push workouts associated with higher estimated strength on the Incline Dumbbell Press?**

Rest days between Push workouts were compared with estimated one-repetition maximum (1RM) performance.

---

### 3. Training Patterns

**How did my training volume and number of sets differ between muscle groups during my Bulk?**

I compared Legs, Push, and Pull training and also examined how my weekly training patterns changed over time.

---

## Data Cleaning

Several cleaning steps were required before the data could be analyzed.

These included:

- Standardizing column names
- Removing blank rows
- Converting dates into R date format
- Standardizing muscle-group names
- Correcting inconsistent exercise names
- Removing observations where repetitions were not recorded
- Handling missing values
- Separating the dataset into Bulk and Cut phases
- Creating weekly and monthly groupings

For example, inconsistent values caused by extra spaces or spelling differences were standardized using functions from `stringr` and `dplyr`.

---

## Feature Engineering

Several new variables were created from the original workout data.

### Training Volume

Training volume was calculated for each recorded set using:

`Volume = Weight × Repetitions`

This was then aggregated into weekly, monthly, exercise-level, and muscle-group summaries.

---

### Estimated One-Rep Max

Strength was estimated using the **Epley Formula**:

`Estimated 1RM = Weight × (1 + Repetitions / 30)`

The estimated 1RM was used to compare Incline Dumbbell Press performance across workouts.

Because this is an estimate rather than a directly tested one-repetition maximum, it should be interpreted as a strength indicator rather than an exact measurement.

---

### Weekly Bodyweight Change

Weekly average bodyweight was calculated during the Cut phase.

Weight change was then calculated using the difference between consecutive weeks with the `lag()` function.

A negative value represents a decrease in average bodyweight.

---

### Rest Days

The number of days between Push workouts was calculated to explore whether additional recovery time was associated with estimated Incline Dumbbell Press strength.

Gaps greater than seven days were treated as likely logging gaps rather than intentional rest periods.

---

## Analysis 1: Weekly Training Volume vs. Bodyweight Change

A linear regression model was used to investigate the relationship between total weekly training volume and weekly bodyweight change during the Cut.

### Original Model Results

- **Slope:** approximately `-0.0000154`
- **p-value:** `0.392`
- **R²:** approximately `0.074`
- **Adjusted R²:** approximately `-0.019`
- **Sample:** approximately 12 weeks

The estimated slope was slightly negative, meaning higher weekly training volume was associated with slightly greater weight loss in the fitted model.

However, the relationship was **not statistically significant**.

With a p-value of approximately 0.392, the analysis did not provide sufficient evidence to conclude that weekly training volume was meaningfully associated with weekly bodyweight change in this dataset.

The very low R² also suggests that weekly training volume alone explained very little of the variation in bodyweight change.

Because the analysis only contained a small number of weeks, the result should be treated as exploratory.

---

## Analysis 2: Rest Days vs. Incline Dumbbell Press Strength

The second analysis explored whether additional rest between Push workouts was associated with higher estimated Incline Dumbbell Press strength.

The original analysis used a linear regression model with estimated 1RM as the response variable and calculated rest days as the predictor.

### Original Model Results

- **Slope:** approximately `+1.69 lbs`
- **p-value:** `0.074`
- **Adjusted R²:** approximately `0.144`
- **Original regression observations:** `17`

The fitted model showed a positive trend, with each additional rest day associated with an estimated increase of approximately 1.69 lbs in Incline Dumbbell Press 1RM.

However, the result did not reach the conventional 0.05 significance level.

Therefore, the analysis did not provide enough statistical evidence to conclude that additional rest was associated with greater strength.

### Important Limitation

When reviewing the project later, I recognized that the original rest-day calculation was performed on set-level workout records.

Because multiple sets can come from the same workout session, some observations in the regression were not fully independent.

A stronger version of this analysis would first aggregate the data to one observation per workout session before calculating the number of days between Push sessions.

This reduces the amount of usable data considerably, meaning that more workout sessions would be needed before drawing a reliable statistical conclusion.

---

## Analysis 3: Training Patterns During the Bulk

The final section of the project focused on descriptive analysis rather than hypothesis testing.

### Muscle-Group Training Volume

Legs produced the highest total recorded training volume.

However, this is partly explained by the fact that many leg exercises use substantially heavier external loads than upper-body exercises.

Because of this, total volume should not necessarily be interpreted as a direct comparison of training difficulty between muscle groups.

---

### Number of Sets

Push workouts contained the largest number of recorded sets.

This matched my personal training preference toward upper-body Push exercises.

Looking at both volume and number of sets provided more context than relying on volume alone.

---

### Training Volume Over Time

Weekly training volume was also examined throughout the Bulk.

The data showed a decline in recorded training volume toward the end of the Bulk and before the transition into the Cut phase.

Possible contributing factors include changes in training frequency, changes in exercise selection, incomplete logging, and schedule changes.

Because these factors were not experimentally controlled, the trend is descriptive rather than causal.

---

## Visualizations

The project uses `ggplot2` to visualize several parts of the training data, including:

- Weekly training volume vs. bodyweight change
- Rest days vs. estimated Incline Dumbbell Press 1RM
- Total training volume by muscle group
- Total sets by muscle group
- Weekly training volume by muscle group
- Monthly training patterns
- Exercise-level training volume
- Exercise-level set frequency

These visualizations were used to explore trends before interpreting the statistical models.

---

## Limitations

This project uses personal observational data rather than data from a controlled experiment.

Several limitations should therefore be considered when interpreting the results:

- The dataset contains missing or incomplete workout logs.
- Some periods contain relatively small sample sizes.
- The original rest-day analysis included repeated sets from the same workout session.
- Bodyweight was recorded on some days but not consistently every day.
- Weekly bodyweight averages were originally calculated using set-level records, meaning days with more logged sets could receive more weight in the weekly average.
- Training volume based on `weight × reps` does not perfectly compare exercises with very different movement patterns.
- Bodyweight exercises are not fully represented by external-load training volume.
- Estimated 1RM is calculated using a formula rather than directly measured.
- Other variables such as nutrition, sleep, stress, and daily activity were not recorded.
- The data are observational, so relationships found in the analysis should not be interpreted as causal effects.

If I revisited the project, I would aggregate repeated sets into workout-session-level observations for the recovery analysis and create one bodyweight observation per day before calculating weekly averages.

---

## What I Learned

This project was primarily a self-directed learning experience.

Through the project I gained experience with:

- Cleaning messy real-world data
- Using `dplyr` for data manipulation
- Using `stringr` to standardize text values
- Working with dates using `lubridate`
- Creating new variables through feature engineering
- Aggregating set-level data into weekly and monthly summaries
- Building visualizations with `ggplot2`
- Applying linear regression to real data
- Interpreting regression coefficients, p-values, and R²
- Recognizing the importance of sample size
- Thinking about the unit of observation in statistical analysis
- Identifying limitations in my own analysis
- Distinguishing exploratory relationships from causal conclusions

One of the most useful parts of this project was being able to revisit my original analysis and recognize areas that could be improved.

Rather than treating the original results as definitive, the project helped me better understand how data structure, sample size, missing observations, and analytical decisions can affect statistical conclusions.

---

## Repository Contents

- `hans_exercise_2025.Rmd` — Full R Markdown analysis, including detailed notes and intermediate steps
- `hans_dano_exercise_data_2025_to_2026.csv` — Workout dataset used in the analysis
- `README.md` — Project overview and summary

---

## About This Project

This project was completed independently as part of my effort to strengthen my skills in R, statistics, and data analysis outside of coursework.

It is intended to document both the analysis itself and my learning process while working with a real dataset that I collected over time.
