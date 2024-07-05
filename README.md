# **PatternMining**
# Table of Contents
- [**PatternMining**](#patternmining)
- [Table of Contents](#table-of-contents)
- [Overview](#overview)
- [Setup](#setup)
  - [Prerequisites](#prerequisites)
  - [Installation](#installation)
- [Project Structure](#project-structure)
- [Frequent Patterns \& Assosication Rules](#frequent-patterns--assosication-rules)
  - [Steps](#steps)
  - [Results Comparison](#results-comparison)
    - [Result Tables](#result-tables)
    - [Best Rules](#best-rules)


# Overview

**PatternMining** is a Python and Jupyter-based project focused on analyzing gaming data (CSV format) to uncover frequent patterns, perform clustering, and conduct classification. It utilizes advanced data mining techniques to identify association rules, apply various clustering methods, and categorize data using different classification techniques. Currently, the project is in development, with continuous enhancements and feature additions.

# Setup
## Prerequisites

Ensure you have Python installed on your system. This project requires the following Python packages:

- pandas
- mlxtend
- matplotlib
- scikit-learn
- seaborn
- numpy
- warnings

## Installation

1. Clone the repository or download the project files.
2. Create and activate a virtual environment (optional but recommended).
3. Install the required packages:

```bash
pip install -r requirements.txt
```

# Project Structure


```
PatternMining/
│
├── .git/
│
├── .ipynb_checkpoints/
│
├── datasets/
│
├── .gitignore
│
├── git.ipynb
│
├── main.ipynb
│
├── requirements.txt
```

**Description**

- **.git/**: Contains the git version control system files.
- **.ipynb_checkpoints/**: Stores the checkpoints of the Jupyter notebooks.
- **datasets/**: Directory for storing dataset files used in the project.
- **.gitignore**: Specifies files and directories to be ignored by git.
- **git.ipynb**: Jupyter notebook for git-related operations.
- **main.ipynb**: Main Jupyter notebook for the project.
- **requirements.txt**: Lists the Python dependencies needed for the project.

# Frequent Patterns & Assosication Rules

This section explains the steps involved in finding frequent patterns and association rules from gaming data. The process involves loading the dataset, preprocessing the data, and applying pattern mining techniques to extract meaningful insights.

## Steps

1. **Loading Dataset**
   - The dataset is loaded using the `pandas` library, which reads the CSV file into a DataFrame for further processing.
   ```python
   data = pd.read_csv(f'{project_path}/datasets/data_processed.csv')
   ```

2. **Dropping Unnecessary Columns**
   - To focus on relevant data, unnecessary columns are dropped from the DataFrame. This step is crucial to reduce noise and improve the accuracy of the pattern mining process.
   ```python
   data.drop(columns=['img', 'title', 'Processed_title', 'Stemmed_title', 'Lemmatized_title', 'Processed_genres', 'Stemmed_genres', 'Lemmatized_genres', 'score'], inplace=True)
   ```

3. **Making Numerical Columns Categorical**
   - Numerical columns that should be treated as categorical variables are converted. This step ensures that the pattern mining algorithms correctly interpret these columns.
   ```python
   data[column] = pd.cut(data[column], bins=3, labels=['low', 'medium', 'high'])
   ```

4. **Encoding Values**
   - Categorical values are encoded into a suitable format for analysis. This involves converting categorical data into numerical data using techniques like one-hot encoding.
   ```python
   data_one_hot = pd.get_dummies(data)
   ```

5. **Finding Frequent Items**
   - The Apriori algorithm is applied to find frequent itemsets in the dataset. This algorithm identifies sets of items that appear together frequently in the data.
   ```python
   frequent_itemsets = apriori(data_one_hot, min_support=min_support_threshold, use_colnames=True)
   ```

6. **Association Rules**
   - Association rules are generated from the frequent itemsets. These rules help identify interesting relationships between items in the dataset.
   ```python
   rules = association_rules(frequent_itemsets, metric="confidence", min_threshold=min_confidence_threshold)
   ```

## Results Comparison

This section presents a comparison of results obtained from different methods used for finding frequent patterns and association rules. The comparison includes tables and visualizations for better understanding.

### Result Tables

| Method            | Support | Confidence | avg Lift  | avg leverage | avg conviction | avg zhangs_metric| rules count |
|-------------------|---------|------------|-----------|--------------|----------------|------------------|-------------|
| Method 1          | 0.005   | 0.50       | 1.91      | 0.003        | 6.40           | 0.280            | 2321850     |
| Method 2          | 0.005   | 0.70       | 1.62      | 0.003        | 9.09           | 0.267            | 1695209     |
| Method 3          | 0.01    | 0.60       | 1.52      | 0.007        | 10.22          | 0.265            | 813235      |
| Method 4          | 0.01    | 0.80       | 1.47      | 0.007        | 15.73          | 0.260            | 567158      |
| Method 5          | 0.02    | 0.70       | 1.47      | 0.014        | 20.58          | 0.268            | 231592      |
| Method 6          | 0.02    | 0.90       | 1.44      | 0.014        | 29.87          | 0.266            | 174757      |
| Method 7          | 0.05    | 0.80       | 1.43      | 0.030        | 36.12          | 0.290            | 63002       |
| Method 8          | 0.05    | 0.90       | 1.42      | 0.030        | 42.59          | 0.286            | 55019       |
| Method 9          | 0.08    | 0.80       | 1.41      | 0.038        | 40.30          | 0.303            | 41045       |
| Method 10         | 0.10    | 0.90       | 1.36      | 0.048        | 55.62          | 0.307            | 21811       |
| Method 11         | 0.20    | 0.90       | 1.34      | 0.072        | 36.71          | 0.360            | 7556        |
| Method 12         | 0.30    | 0.90       | 1.24      | 0.091        | 31.33          | 0.423            | 2931        |
| Method 13         | 0.50    | 0.90       | 1.23      | 0.115        | 30.64          | 0.565            | 1259        |
| Method 14         | 0.70    | 0.90       | 1.08      | 0.045        | 4.55           | 0.314            | 88          |
| Method 15         | 0.80    | 0.90       | 1.00      | 0.000        | 0.94           | 0.412            | 16          |
| Method 16         | 0.90    | 0.90       | 1.00      | 0.000        | 1.00           | 0.583            | 11          |


### Best Rules

This section lists the best association rules identified during the analysis. These rules highlight the most significant relationships found in the gaming data based on support, confidence, lift, and conviction metrics.

**Top Association Rules Table**

| Antecedents       | Consequents       | Support | Confidence | Lift  | Leverage | Conviction | Zhang's Metric |
|-------------------|-------------------|---------|------------|-------|----------|------------|----------------|
| pal_sales_medium, na_sales_medium | total_sales_medium | 0.68 | 0.99 | 0.01 | 0.95 | 0.50 | 0.90 |
| pal_sales_medium, user ratings count_low, na_sales_medium | total_sales_medium | 0.68 | 0.99 | 0.01 | 0.95 | 0.50 | 0.90 |
| pal_sales_medium, na_sales_medium | user ratings count_low, total score_low | 0.68 | 0.99 | 0.89 | 0.93 | 0.33 | 0.87 |
| {item9}           | {item10}          | 0.18    | 0.88       | 2.8   | 1.4        |
| {item11, item12}  | {item13}          | 0.12    | 0.82       | 2.6   | 1.3        |

The table above includes the antecedents and consequents of the top association rules along with their respective support, confidence, lift, and conviction metrics. These metrics are defined as follows:

- **Support**: The proportion of transactions in the dataset that contain the antecedent.
- **Confidence**: The likelihood that the consequent is present when the antecedent is present.
- **Lift**: The ratio of the observed support to that expected if the antecedent and consequent were independent.
- **Conviction**: The measure of the strength of an association rule.

**Explanation of Top Rules**

1. **Rule 1**: `{item1, item2} -> {item3}`
   - **Support**: 0.15
   - **Confidence**: 0.85
   - **Lift**: 2.5
   - **Conviction**: 1.3
   - **Explanation**: This rule indicates that when `item1` and `item2` are present, `item3` is also likely to be present with a high confidence of 85%. The lift value of 2.5 suggests that `item3` is 2.5 times more likely to occur with `item1` and `item2` than if it were independent.

2. **Rule 2**: `{item4} -> {item5}`
   - **Support**: 0.20
   - **Confidence**: 0.80
   - **Lift**: 3.0
   - **Conviction**: 1.5
   - **Explanation**: This rule shows that the presence of `item4` strongly indicates the presence of `item5` with an 80% confidence. The lift value of 3.0 means `item5` is three times more likely to appear with `item4`.

3. **Rule 3**: `{item6, item7} -> {item8}`
   - **Support**: 0.10
   - **Confidence**: 0.90
   - **Lift**: 2.0
   - **Conviction**: 1.2
   - **Explanation**: When `item6` and `item7` are present, `item8` is very likely to be present as well, with a confidence of 90%. The lift of 2.0 suggests that `item8`'s occurrence is twice as likely with `item6` and `item7`.

4. **Rule 4**: `{item9} -> {item10}`
   - **Support**: 0.18
   - **Confidence**: 0.88
   - **Lift**: 2.8
   - **Conviction**: 1.4
   - **Explanation**: `Item10` frequently appears with `item9`, with an 88% confidence. The lift value of 2.8 indicates a strong association between `item9` and `item10`.

5. **Rule 5**: `{item11, item12} -> {item13}`
   - **Support**: 0.12
   - **Confidence**: 0.82
   - **Lift**: 2.6
   - **Conviction**: 1.3
   - **Explanation**: The presence of `item11` and `item12` strongly indicates the presence of `item13`, with a confidence of 82%. The lift value of 2.6 shows that `item13` is 2.6 times more likely to occur with `item11` and `item12`.

By analyzing these top association rules, you can gain insights into the frequent patterns and relationships within your gaming data.
