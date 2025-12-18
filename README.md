# M10 Assignment: Frequentist Hypothesis Tests 

## Overview

Throughout the semester, you've worked on assignments where we used various computational statistical techniques, such as permutation tests and bootstrapping, to do statistical inference. In this week's assignment, you compare the results on earlier assignments with frequentist approaches based on the CLT. As a reminder, here are some of the previous analyses you've done: 

*  **Basic Data Manipulation** (M1): looking at prices of F-150s across various midwestern cities. 
*  **Only One Test** (M4): hypothesis tests based on data you requested from the Craigslist data set.
*  **Central Limit Theorem** (M5): Prices of Hondas in California.
*  **Permutation Tests** (M6): tests on satisfaction from a survey of tech company employees. 
*  **Bootstrapping** (M8): analysis of data from the Washington State Employee Credit Union membership. 

Primarily, this assigment is going to evaluate two things, both of which are important: 

1. Your ability to carry out and interpret tests of hypotheses or create confidence intervals based on the Central Limit Theorem. While this approach is not my preferred technique, it's important to know to work with others out in the real world. 
2. Your ability to keep your code and data flows organized. This assignment asks you to revisit previous assignments and adopt code from them. This is a real challenge! We often finish projects in a rush, so it can be difficult to re-use that work. In this assignment, you'll either pat yourself on the back for keep well-organized repositories or lament that lack of organization. 

## Instructions & Policies
- **AI use:** Same policy as recent assignments — you may ask AI to clarify syntax or logic, but do not paste complete solutions. 
- **Output:** Submitted notebooks should be run top-to-bottom without errors. Restart, clear outputs, and Run All before turning in your work.
- **Documentation:** Each task needs (a) a short recap of your resampling work including results, (b) the new frequentist analysis, and (c) a brief written interpretation that compares the two approaches.
- **Data hygiene:** Keep sensitive or large CSVs out of Git. Reference them via local paths or environment variables.


## Before You Start
1. Locate your original notebooks for the assignments listed above. You'll be reusing portions of the code from those assignments. 
2. Make sure the raw CSV files live outside of this repo (or are ignored by Git). Update the paths in `hypothesis-tests.ipynb` to wherever you store them locally.
3. Skim the “Frequentist toolbox reminder” cell inside the notebook so you know which functions to import.


## Tasks 

From the table below, choose five tasks to complete. Of the five, choose three hypothesis tests and two confidence interval tasks. For each chosen task, you'll do a permutation or bootstrap approach and the CLT-inspired approach described in class and the in-class exercise.

For **one** of your confidence interval tasks, choose a statistic other than the mean or proportion statistics in the rest of the assignment. Use bootstrapping to estimate uncertainty of that statistic. Bonus points if that metric is somehow interesting. 


| Assignment Name | Data Set | Analysis Type | Analysis |
| --- | --- | --- | --- |
| Basic Data Manipulation | `car_listings.csv` – Craigslist listings across 12 Midwest cities | Hypothesis Test | Filter to Ford F-150s from Duluth and Minneapolis, clean prices, and test whether Duluth’s mean asking price exceeds Minneapolis using a difference-in-means statistic with permutation resampling. |
| Basic Data Manipulation | `car_listings.csv` – Craigslist listings across 12 Midwest cities | Uncertainty Estimation (CI) | Build 95% CIs for F-150 prices in each city by sampling within location (or using bootstrap) so students can compare price uncertainty geographically. |
| CLT | `california_hondas.txt` – census of ~111k Honda listings in California | Uncertainty Estimation (CI) | Use repeated samples of the most popular Honda models (perhaps top 10?; you can decide) to form CLT-based CIs for mean prices, highlighting how sampling distributions tighten with larger sample sizes. |
| Only One Test (OOT) | Self-serve car listings pull (student-defined filters, up to 100k rows) | Hypothesis Test | Recreate the original OOT question but replace informal sampling with (a) permutation-based null simulations and (b) CLT-standard-error calculations to show both inference routes. |
| Permutation Tests | `satisfaction_survey.txt` – employee satisfaction survey with gender, tenure, location | Hypothesis Test | Test whether the chosen gender’s mean satisfaction differs from the combined other genders by shuffling gender labels to get a null distribution for the mean difference. |
| Permutation Tests | `satisfaction_survey.txt` – employee satisfaction survey with gender, tenure, location | Hypothesis Test | Compare the fraction of respondents with satisfaction > 4 for one gender versus others using a permutation test on the binary “satisfaction > 4” indicator. |
| Permutation Tests | `satisfaction_survey.txt` – employee satisfaction survey with gender, tenure, location | Uncertainty Estimation (CI) | Generate bootstrap CIs for mean satisfaction within each gender group to quantify uncertainty around the observed differences. |
| Bootstrap | Credit union member survey (2,421 WA respondents with region, progressivism, focal values) | Hypothesis Test | Compute progressivism scores and test whether a target region’s mean differs from the rest using bootstrap differences (or permutation) to form the reference distribution. |
| Bootstrap | Credit union member survey (2,421 WA respondents with region, progressivism, focal values) | Hypothesis Test | Test whether the proportion choosing “Education” as their main focal value differs between east and west regions by bootstrapping/permuting the education indicator across the two region groups. |


## Deliverables
- A completed `hypothesis-tests.ipynb` notebook that documents all five tasks above (resampling recap + frequentist redo + interpretation).
- Any supporting figures or tables embedded directly in the notebook.

## Submission Checklist
- [ ] All five task sections filled out with both resampling summaries and frequentist analyses.
- [ ] Notebook runs from top to bottom after Restart & Run All (no errors, no stray debug cells).
- [ ] Conclusions explicitly compare simulation-based and analytic results.
- [ ] Raw data files remain outside the repo or are `.gitignore`’d.
- [ ] Notebook saved with clean outputs before commit & push.

## Note from John

Just putting in a commit so my code stops flagging this as "needing review".

## Feedback 

In task one, where I ask for the CLT, I'm not looking for this: 
```
sample_sizes = [30]
n_samples = 1000
results = []

# Step 4: CLT Simulation 
for n in sample_sizes:
    sample_means = []

    for _ in range(n_samples):
        sample = np.random.choice(mpls_f150_price, size=n, replace=True)
        sample_means.append(np.mean(sample))

    sample_means = np.array(sample_means)

    # Empirical Standard Error
    empirical_se = np.std(sample_means, ddof=1)

    # Theoretical SE (from CLT)
    theoretical_se = np.std(mpls_f150_price, ddof=1) / np.sqrt(n)

    # Store results
    results.append([n, empirical_se, theoretical_se])

    # ---- Plot Sampling Distribution ----
    plt.figure(figsize=(8,4))
    plt.hist(sample_means, bins=30, edgecolor='black')
    plt.title(f"Sampling Distribution of Mean mpls_f150_price(n={n})")
    plt.xlabel("Sample Mean Price")
    plt.ylabel("Frequency")
    plt.grid(alpha=0.2)
    plt.show()
```

The idea is to use the CLT code from the exercises. In this case you'd do at t-test and you should get a very small p-value there. Then you'll have something to directly compare. 

You do this correctly further down, but don't have much commentary. Make that fix for Task 1, add your commentary and reflection, and you should be done. 
