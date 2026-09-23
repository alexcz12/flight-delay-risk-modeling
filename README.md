# Flight Delay Risk Modeling

A predictive modeling project analyzing flight departure delays using public airline performance data, with an emphasis on **probability calibration** over raw accuracy, and a practical application to flight scheduling decisions.

This work was completed as a course project at the University of Pittsburgh, reflecting a broader interest in applying data science and statistical modeling to real-world operational challenges.

## Project Overview

Using historical flight performance data, this project builds models to classify flights into three delay categories (`not_delayed`, `short_delay`, `long_delay`) and evaluates which model produces the most **trustworthy probability estimates** — not just the highest accuracy. A well-calibrated model was then used to simulate delay-risk across different scheduled departure times for a specific flight, demonstrating how the model could support real scheduling decisions.

**Data source:** [U.S. Bureau of Transportation Statistics — Airline Service Quality Performance (Form 234) Time Data](https://www.bts.gov/browse-statistical-products-and-data/bts-publications/airline-service-quality-performance-234-time), covering flights through two hub airports (ORD and PIT) over roughly a one-year period. All data used is publicly available; no proprietary or internal airline data was used.

## Repository Structure

```
├── 01_exploratory_analysis/         # Initial data exploration and CoNVO problem framing
├── 02_preliminary_modeling/         # First-pass modeling: logistic regression, random forest, boosting
└── 03_final_model_and_simulation/   # Final calibrated model + flight scheduling application
```

Each folder contains both a `.Rmd` (source code) and rendered `.pdf` report/presentation. The PDFs are the easiest way to review the work directly on GitHub (click to preview); the `.Rmd` files contain the underlying R code.

### 01 — Exploratory Analysis
- Defines the project using a CoNVO (Context, Need, Vision, Outcome) framework
- Explores delay patterns by time of day, day of week, and airport
- Identifies "bank" scheduling structure at ORD (clustered departure waves) as a likely driver of delay risk

### 02 — Preliminary Modeling
- First-pass models: Logistic Regression, Random Forest, and Gradient Boosting
- Compares models using ROC, sensitivity, and specificity
- Introduces calibration as an evaluation criterion, alongside standard accuracy metrics

### 03 — Final Model and Simulation
- Extends modeling to both ORD and PIT, with a multinomial outcome (`not_delayed` / `short_delay` / `long_delay`)
- Engineers a **congestion feature**: the number of flights scheduled to depart in the 30 minutes prior to a given flight, capturing the effect of ORD's bank-based scheduling structure
- Compares calibration across all three models; **Gradient Boosting was selected as the final model** based on calibration quality (i.e., whether a predicted 30% delay probability actually corresponds to a ~30% observed delay rate), not just raw classification accuracy
- **Applied example:** uses the calibrated model to simulate an underperforming flight's delay-risk across a range of alternative departure times, identifying a reschedule window that reduces projected delay risk
- Discusses data limitations encountered (e.g., raw `.asc`-format BTS extracts) and outlines future directions (additional features such as aircraft type, weather, and extending the analysis to more airports)

## Methods Used
- **Languages/Tools:** R (tidyverse, caret, ggplot2)
- **Modeling:** Multinomial Logistic Regression, Random Forest, Gradient Boosting
- **Evaluation:** ROC/AUC, sensitivity/specificity, and probability calibration analysis
- **Feature engineering:** time-window-based congestion metric derived from scheduling density

## Notes
- Raw data and trained model files are not included in this repository due to file size; the code to generate both is included in full.
- AI tools were used selectively to assist with plot and table formatting; all analysis, modeling decisions, and interpretation are my own.
- This project uses publicly available BTS data and is not affiliated with or representative of any airline's internal systems or data.
