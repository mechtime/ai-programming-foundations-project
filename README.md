# Airbnb NYC Rental Prices Analysis

## Project Description

This project performs exploratory data analysis on the Airbnb NYC 2019 dataset to identify pricing patterns in the New York City short-term rental market. The analysis includes data cleaning, statistical summaries, and visualizations to uncover relationships between listing features and rental prices.

**Dataset:** [Airbnb NYC 2019](https://www.kaggle.com/datasets/dgomonov/new-york-city-airbnb-open-data) (AB_NYC_2019.csv)

## How to Run the Project

### Install Dependencies

```bash
pip install -r requirements.txt
```

### Run the Notebook

1. Open the project folder in VS Code or Jupyter
2. Open `data_workflow.ipynb`
3. Run all cells from top to bottom (Cell > Run All)

### Required Files

- `data_workflow.ipynb` - Main analysis notebook
- `AB_NYC_2019.csv` - Dataset (must be in same directory)
- `requirements.txt` - Python dependencies

## Reflection Questions

### Bias Awareness

Poor data cleaning decisions can introduce bias in several ways:

**Missing Value Handling:** Using median imputation assumes data are missing at random. If reviews_per_month is missing for listings that have never been booked (rather than randomly), filling with the median misrepresents these properties and could skew analysis of review patterns.

**Outlier Removal:** Removing the top and bottom 1% of prices systematically excludes both very affordable listings (potentially in underserved neighborhoods) and luxury properties. If low-priced listings are concentrated in certain boroughs like the Bronx, the analysis may underrepresent those communities and their actual pricing patterns.

**Geographic Representation:** Areas with fewer listings have less statistical weight, potentially causing the analysis to favor patterns in high-density areas like Manhattan while underrepresenting outer boroughs.

### Future Integration Reflections

**How would you modify this workflow for a machine learning project?**

For ML integration, I would add: (1) train-test split before any cleaning to prevent data leakage, (2) one-hot encoding for categorical variables like room_type and neighbourhood_group, (3) feature scaling for numeric columns, (4) scikit-learn pipelines to chain preprocessing with model training, and (5) cross-validation for robust performance estimation.

**What additional preprocessing would be needed for neural network training?**

Neural networks would require: (1) normalization of all numeric features to 0-1 or standard scaling, (2) embedding layers for high-cardinality categorical variables like neighbourhood (221 unique values), (3) text preprocessing if using listing names/descriptions, (4) batch preparation for GPU processing, and (5) log transformation of the right-skewed price target.

**What parts of this project could be automated using agentic AI?**

Agentic AI could automate: (1) data profiling to detect types, missing values, and outliers, (2) cleaning strategy selection based on data characteristics, (3) feature importance evaluation and selection, (4) automatic visualization generation based on data types, (5) initial interpretation drafting for statistical results, and (6) pipeline monitoring for data drift in production.
