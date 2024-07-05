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

This section lists the best association rules identified during the analysis. These rules highlight the most significant relationships found in the gaming data based on support, confidence, lift, leverage, conviction, and Zhang's metric.

**Top Association Rules Table**

| Antecedents                        | Consequents                | Support | Confidence | Lift  | Leverage | Conviction | Zhang's Metric |
|------------------------------------|----------------------------|---------|------------|-------|----------|------------|----------------|
| pal_sales_medium, na_sales_medium  | total_sales_medium         | 0.68    | 0.99       | 0.01  | 0.95     | 0.50       | 0.90           |
| pal_sales_medium, user ratings count_low, na_sales_medium | total_sales_medium | 0.68 | 0.99 | 0.01 | 0.95 | 0.50 | 0.90 |
| pal_sales_medium, na_sales_medium  | user ratings count_low, total score_low | 0.68 | 0.99 | 0.89 | 0.93 | 0.33 | 0.87 |
| total score_low                    | metascore_count_low        | 0.93    | 0.93       | 0.00  | 0.00     | 0.00       | 1.0            |
| user ratings count_low, na_sales_medium | total_sales_medium, total score_low | 0.71 | 0.97 | 1.0 | 1.0 | 0.92 | 0.93 |
| total_sales_medium                 | na_sales_medium, total score_low | 0.71 | 0.97 | 0.99 | 0.99 | 0.99 | 0.93 |

The table above includes the antecedents and consequents of the top association rules along with their respective support, confidence, lift, leverage, conviction, and Zhang's metric. These metrics are defined as follows:

- **Support**: The proportion of transactions in the dataset that contain the antecedent.
- **Confidence**: The likelihood that the consequent is present when the antecedent is present.
- **Lift**: The ratio of the observed support to that expected if the antecedent and consequent were independent.
- **Leverage**: The difference between the observed frequency of a rule and the expected frequency if the antecedent and consequent were independent.
- **Conviction**: The measure of the strength of an association rule, indicating how often the rule makes an incorrect prediction.
- **Zhang's Metric**: A measure that considers both support and confidence, giving a more balanced view of the rule's interestingness.

**Explanation of Top Rules**

1. **Rule 1**: `{pal_sales_medium, na_sales_medium} -> {total_sales_medium}`
   - **Support**: 0.68
   - **Confidence**: 0.99
   - **Lift**: 0.01
   - **Leverage**: 0.95
   - **Conviction**: 0.50
   - **Zhang's Metric**: 0.90
   - **Explanation**: This rule indicates that when `pal_sales_medium` and `na_sales_medium` are present, `total_sales_medium` is almost always present with a confidence of 99%. The high leverage value of 0.95 suggests a strong association between these variables.

2. **Rule 2**: `{pal_sales_medium, user ratings count_low, na_sales_medium} -> {total_sales_medium}`
   - **Support**: 0.68
   - **Confidence**: 0.99
   - **Lift**: 0.01
   - **Leverage**: 0.95
   - **Conviction**: 0.50
   - **Zhang's Metric**: 0.90
   - **Explanation**: This rule shows that the presence of `pal_sales_medium`, `user ratings count_low`, and `na_sales_medium` strongly indicates the presence of `total_sales_medium`.

3. **Rule 3**: `{pal_sales_medium, na_sales_medium} -> {user ratings count_low, total score_low}`
   - **Support**: 0.68
   - **Confidence**: 0.99
   - **Lift**: 0.89
   - **Leverage**: 0.93
   - **Conviction**: 0.33
   - **Zhang's Metric**: 0.87
   - **Explanation**: When `pal_sales_medium` and `na_sales_medium` are present, `user ratings count_low` and `total score_low` are also likely to be present with a confidence of 99%.

4. **Rule 4**: `{total score_low} -> {metascore_count_low}`
   - **Support**: 0.93
   - **Confidence**: 0.93
   - **Lift**: 0.00
   - **Leverage**: 0.00
   - **Conviction**: 0.00
   - **Zhang's Metric**: 1.0
   - **Explanation**: This rule shows that `total score_low` is almost always associated with `metascore_count_low`, with a high support and confidence of 93%.

5. **Rule 5**: `{user ratings count_low, na_sales_medium} -> {total_sales_medium, total score_low}`
   - **Support**: 0.71
   - **Confidence**: 0.97
   - **Lift**: 1.0
   - **Leverage**: 1.0
   - **Conviction**: 0.92
   - **Zhang's Metric**: 0.93
   - **Explanation**: This rule indicates a strong association between `user ratings count_low`, `na_sales_medium`, and `total_sales_medium`, `total score_low`.

6. **Rule 6**: `{total_sales_medium} -> {na_sales_medium, total score_low}`
   - **Support**: 0.71
   - **Confidence**: 0.97
   - **Lift**: 0.99
   - **Leverage**: 0.99
   - **Conviction**: 0.99
   - **Zhang's Metric**: 0.93
   - **Explanation**: When `total_sales_medium` is present, `na_sales_medium` and `total score_low` are also very likely to be present, with a high confidence of 97%.

