# Airbnb NYC Rental Prices Analysis

**Author:** David Graham

**Course:** AI Programming Foundations Capstone

## Project Description

This project performs an exploratory data analysis (EDA) on the Airbnb NYC 2019 dataset to uncover patterns and relationships between listing features and rental prices. The analysis includes data cleaning, statistical summaries, grouped analysis, and visualizations to identify key factors that influence pricing in the New York City short-term rental market.

### Dataset

- **Source:** Airbnb NYC 2019 Listings (AB_NYC_2019.csv)
- **Records:** 48,895 listings
- **Features:** 16 columns including price, location, room type, reviews, and availability

### Key Findings

- Manhattan commands the highest average rental prices, followed by Brooklyn
- Room type is the strongest categorical predictor of price (Entire home > Private room > Shared room)
- Price distribution is right-skewed with most listings between $50-150 per night
- Numeric features show weak linear correlations with price, suggesting categorical factors dominate

## Reproducibility Instructions

### Prerequisites

- Python 3.10 or higher
- pip package manager

### Setup

1. Clone the repository:
   ```bash
   git clone https://github.com/mechtime/ai-programming-foundations-project.git
   cd ai-programming-foundations-project
   ```

2. Create and activate a virtual environment (recommended):
   ```bash
   python -m venv venv
   # Windows
   venv\Scripts\activate
   # macOS/Linux
   source venv/bin/activate
   ```

3. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```

4. Launch Jupyter Notebook:
   ```bash
   jupyter notebook data_workflow.ipynb
   ```

5. Run all cells in order from top to bottom.

### Required Files

- `data_workflow.ipynb` - Main analysis notebook
- `AB_NYC_2019.csv` - Dataset (must be in same directory as notebook)
- `requirements.txt` - Python dependencies

## Reflection Questions

### Bias Awareness: Where Could Poor Data Cleaning Introduce Bias?

Poor data cleaning decisions can introduce or amplify bias in several ways in this analysis:

**Missing Value Handling:** The dataset contains missing values in `reviews_per_month` for listings that have never been reviewed. Filling these with the median assumes these listings are similar to reviewed ones, but they may represent newer listings, inactive listings, or listings in less desirable locations. This could mask systematic differences between reviewed and unreviewed properties.

**Outlier Removal:** By removing the top and bottom 1% of prices, we exclude both very cheap listings (potentially in underserved neighborhoods or with data entry errors) and luxury properties. This decision systematically removes data from the extremes of the market. If low-priced listings are concentrated in certain boroughs or neighborhoods, our analysis may underrepresent those communities and their actual pricing patterns.

**Geographic Representation:** The dataset may not uniformly represent all NYC neighborhoods. Areas with fewer listings have less statistical weight, potentially causing the analysis to favor patterns in high-listing-density areas like Manhattan and Brooklyn while underrepresenting the Bronx and Staten Island.

**Temporal Bias:** Using median imputation for `last_review` dates treats listings without reviews as if they were reviewed at the median date, obscuring the actual timeline of listing activity and potentially hiding patterns related to seasonality or market changes.

### Future Integration Reflections

#### How would you modify this workflow for a machine learning project?

To adapt this workflow for machine learning, I would make the following modifications:

1. **Feature Engineering:** Create new features from existing data, such as extracting neighborhood-level statistics, calculating distance to landmarks, or deriving host experience metrics from listing counts.

2. **Train-Test Split:** Before any data cleaning or transformation, split the data into training and test sets to prevent data leakage. All transformations (scaling, encoding, imputation) should be fit only on training data.

3. **Encoding Categorical Variables:** Convert categorical columns like `neighbourhood_group`, `room_type`, and `neighbourhood` using one-hot encoding or target encoding for use in ML models.

4. **Feature Scaling:** Normalize or standardize numeric features so that variables with large ranges do not dominate model training.

5. **Cross-Validation:** Implement k-fold cross-validation to better estimate model performance and reduce overfitting.

6. **Pipeline Construction:** Use scikit-learn pipelines to chain preprocessing steps with model training, ensuring reproducibility and preventing data leakage.

#### What additional preprocessing would be needed for neural network training?

Neural networks have specific data requirements that would necessitate additional preprocessing:

1. **Normalization:** Scale all numeric features to a common range (typically 0-1 or standardized to mean=0, std=1) since neural networks are sensitive to feature magnitudes.

2. **Embedding Layers:** For high-cardinality categorical variables like `neighbourhood` (221 unique values), use embedding layers instead of one-hot encoding to learn dense representations and reduce dimensionality.

3. **Handling Text Data:** If using listing names or descriptions, implement text preprocessing including tokenization, padding sequences to uniform length, and creating vocabulary embeddings.

4. **Batch Preparation:** Structure data into batches for efficient GPU processing, potentially using data generators for large datasets that do not fit in memory.

5. **Data Augmentation:** Consider augmentation techniques if the dataset is small, though this is more applicable to image or text data than tabular data.

6. **Target Transformation:** Apply log transformation to the price target variable to handle right-skewed distribution and improve model convergence.

#### What parts of this project could be automated using agentic AI?

Several components of this data workflow could benefit from agentic AI automation:

1. **Automated Data Profiling:** An agent could automatically detect data types, identify missing values, find outliers, and generate initial data quality reports without manual inspection.

2. **Cleaning Strategy Selection:** An agent could analyze the nature and patterns of missing data, then recommend or automatically apply appropriate imputation strategies based on the data characteristics.

3. **Feature Selection:** An agent could evaluate feature importance, detect multicollinearity, and suggest which features to include or exclude based on their predictive value and redundancy.

4. **Visualization Generation:** An agent could automatically generate relevant visualizations based on data types and relationships discovered during profiling, selecting appropriate chart types for each analysis.

5. **Report Writing:** An agent could draft initial interpretations of statistical results and visualizations, identifying key patterns and anomalies for human review.

6. **Code Generation:** An agent could generate boilerplate code for common preprocessing tasks, adapting to the specific dataset schema and identified data quality issues.

7. **Pipeline Monitoring:** In a production setting, an agent could monitor data drift, detect when retraining is needed, and flag unusual patterns in incoming data.

## Project Structure

```
ai-programming-foundations-project/
├── data_workflow.ipynb      # Main analysis notebook
├── AB_NYC_2019.csv          # Dataset
├── requirements.txt         # Python dependencies
├── README.md                # This file
└── .gitignore               # Git ignore rules
```

## License

This project is submitted as coursework for the AI Programming Foundations Capstone.
