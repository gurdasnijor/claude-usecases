---
name: Data Analysis Assistant
description: Expert data analyst that explores datasets, performs statistical analysis, identifies patterns, and generates insights from CSV, JSON, and other structured data formats
version: 1.0.0
author: 360 Social Impact Studios
created: 2025-12-07
updated: 2025-12-07
status: production
category: data-analytics
tags: [data-analysis, statistics, csv, json, pandas, visualization, insights, exploration]
tools: [Read, Write, Edit, Bash]
integrations: [technical-writer, database-schema-designer]
outputs: [analysis-reports, statistical-summaries, data-insights, visualization-recommendations]
complexity: medium
---

# Data Analysis Assistant

## Purpose

Explore and analyze structured data to extract meaningful insights. Perform statistical analysis, identify patterns and anomalies, and provide actionable recommendations based on data findings.

---

## Activation Triggers

Use this skill when the user:
- Wants to "analyze this data" or "explore this dataset"
- Needs "statistical analysis" or "summary statistics"
- Asks to "find patterns" or "identify trends"
- Wants to "clean data" or "handle missing values"
- Needs "correlation analysis" or "distribution analysis"
- Asks about "data quality" issues
- Wants "visualization recommendations"

---

## Supported Formats

### Primary
- **CSV** - Comma-separated values
- **JSON** - JavaScript Object Notation (records, nested)
- **Excel** - .xlsx files (via pandas)

### Additional
- TSV - Tab-separated values
- Parquet - Columnar storage
- SQL query results
- API response data

---

## Execution Workflow

### Phase 1: Data Understanding

**Step 1.1: Initial Assessment**

```python
# Standard exploration workflow
import pandas as pd

# Load data
df = pd.read_csv('data.csv')

# Basic info
print(f"Shape: {df.shape}")  # (rows, columns)
print(f"Columns: {df.columns.tolist()}")
print(f"Data types:\n{df.dtypes}")

# First look
df.head()
df.tail()
df.sample(5)
```

**Step 1.2: Data Profile Report**

```
Dataset Profile:
├── Rows: [count]
├── Columns: [count]
├── Memory usage: [size]
│
├── Column Types:
│   ├── Numeric: [count] columns
│   ├── Categorical: [count] columns
│   ├── DateTime: [count] columns
│   └── Other: [count] columns
│
├── Missing Values:
│   ├── Total cells with missing: [count] ([%])
│   └── Columns with missing: [list]
│
└── Potential Issues:
    ├── Duplicate rows: [count]
    ├── Constant columns: [list]
    └── High cardinality: [list]
```

---

### Phase 2: Statistical Analysis

**Step 2.1: Descriptive Statistics**

```python
# Numeric columns
df.describe()

# Extended statistics
numeric_stats = df.describe(percentiles=[.01, .05, .25, .5, .75, .95, .99])

# For each numeric column:
stats = {
    'count': df[col].count(),
    'missing': df[col].isna().sum(),
    'mean': df[col].mean(),
    'std': df[col].std(),
    'min': df[col].min(),
    'q1': df[col].quantile(0.25),
    'median': df[col].median(),
    'q3': df[col].quantile(0.75),
    'max': df[col].max(),
    'skewness': df[col].skew(),
    'kurtosis': df[col].kurtosis()
}
```

**Step 2.2: Categorical Analysis**

```python
# Value counts for each categorical column
for col in categorical_columns:
    print(f"\n{col}:")
    print(f"  Unique values: {df[col].nunique()}")
    print(f"  Top 5:\n{df[col].value_counts().head()}")
    print(f"  Missing: {df[col].isna().sum()}")
```

**Step 2.3: Distribution Analysis**

```python
# Check distribution type
from scipy import stats

# Normality test
stat, p_value = stats.normaltest(df[col].dropna())
is_normal = p_value > 0.05

# Distribution characteristics
skewness = df[col].skew()
# |skew| < 0.5: approximately symmetric
# 0.5 < |skew| < 1: moderately skewed
# |skew| > 1: highly skewed

kurtosis = df[col].kurtosis()
# kurtosis ≈ 0: normal-like tails
# kurtosis > 0: heavy tails (outlier-prone)
# kurtosis < 0: light tails
```

**Step 2.4: Correlation Analysis**

```python
# Correlation matrix
corr_matrix = df[numeric_columns].corr()

# Find strong correlations
strong_correlations = []
for i, col1 in enumerate(numeric_columns):
    for j, col2 in enumerate(numeric_columns):
        if i < j:  # Upper triangle only
            corr = corr_matrix.loc[col1, col2]
            if abs(corr) > 0.7:  # Strong correlation threshold
                strong_correlations.append({
                    'columns': (col1, col2),
                    'correlation': corr,
                    'strength': 'strong positive' if corr > 0 else 'strong negative'
                })
```

---

### Phase 3: Data Quality Assessment

**Step 3.1: Missing Value Analysis**

```python
# Missing value summary
missing_summary = pd.DataFrame({
    'column': df.columns,
    'missing_count': df.isna().sum(),
    'missing_percent': (df.isna().sum() / len(df) * 100).round(2)
}).sort_values('missing_count', ascending=False)

# Missing value patterns
# Are values missing randomly or systematically?
```

**Step 3.2: Outlier Detection**

```python
# IQR method
def detect_outliers_iqr(series):
    Q1 = series.quantile(0.25)
    Q3 = series.quantile(0.75)
    IQR = Q3 - Q1
    lower_bound = Q1 - 1.5 * IQR
    upper_bound = Q3 + 1.5 * IQR
    outliers = series[(series < lower_bound) | (series > upper_bound)]
    return {
        'count': len(outliers),
        'percent': len(outliers) / len(series) * 100,
        'lower_bound': lower_bound,
        'upper_bound': upper_bound
    }

# Z-score method
def detect_outliers_zscore(series, threshold=3):
    z_scores = (series - series.mean()) / series.std()
    outliers = series[abs(z_scores) > threshold]
    return len(outliers)
```

**Step 3.3: Data Quality Score**

```
Data Quality Assessment:
│
├── Completeness: [score]%
│   └── Based on non-null values
│
├── Uniqueness: [score]%
│   └── Based on duplicate detection
│
├── Validity: [score]%
│   └── Based on value constraints
│
├── Consistency: [score]%
│   └── Based on format consistency
│
└── Overall Quality Score: [weighted average]
```

---

### Phase 4: Pattern Recognition

**Step 4.1: Trend Analysis**

```python
# For time series data
df['date'] = pd.to_datetime(df['date'])
df = df.sort_values('date')

# Rolling statistics
df['rolling_mean'] = df['value'].rolling(window=7).mean()
df['rolling_std'] = df['value'].rolling(window=7).std()

# Trend direction
from scipy import stats
slope, intercept, r_value, p_value, std_err = stats.linregress(
    range(len(df)), df['value']
)
trend = 'increasing' if slope > 0 else 'decreasing'
```

**Step 4.2: Segmentation Analysis**

```python
# Group-based analysis
segments = df.groupby('category').agg({
    'value': ['mean', 'median', 'std', 'count'],
    'other_metric': ['mean', 'sum']
})

# Identify significant differences
for segment in df['category'].unique():
    segment_data = df[df['category'] == segment]['value']
    rest_data = df[df['category'] != segment]['value']
    stat, p_value = stats.ttest_ind(segment_data, rest_data)
    if p_value < 0.05:
        print(f"{segment} is significantly different from others")
```

**Step 4.3: Anomaly Detection**

```python
# Statistical anomalies
def find_anomalies(df, column, method='zscore', threshold=3):
    if method == 'zscore':
        z_scores = (df[column] - df[column].mean()) / df[column].std()
        anomalies = df[abs(z_scores) > threshold]
    elif method == 'iqr':
        Q1, Q3 = df[column].quantile([0.25, 0.75])
        IQR = Q3 - Q1
        anomalies = df[(df[column] < Q1 - 1.5*IQR) | (df[column] > Q3 + 1.5*IQR)]
    return anomalies

# Time-based anomalies (sudden changes)
df['pct_change'] = df['value'].pct_change()
sudden_changes = df[abs(df['pct_change']) > 0.5]  # >50% change
```

---

### Phase 5: Insight Generation

**Step 5.1: Key Findings Template**

```markdown
## Data Analysis Report

### Executive Summary
[2-3 sentence overview of the most important findings]

### Dataset Overview
- **Records:** [count]
- **Features:** [count]
- **Time Range:** [if applicable]
- **Data Quality Score:** [score]%

### Key Findings

#### 1. [Finding Title]
**Observation:** [What was observed]
**Evidence:** [Supporting statistics/data]
**Implication:** [Why this matters]
**Recommendation:** [Suggested action]

#### 2. [Finding Title]
...

### Statistical Highlights

| Metric | Value | Interpretation |
|--------|-------|----------------|
| [metric] | [value] | [meaning] |

### Correlations of Note
- [Column A] and [Column B]: r = [value] ([interpretation])

### Data Quality Issues
1. [Issue with count/percentage and recommendation]

### Recommendations
1. [Actionable recommendation]
2. [Actionable recommendation]

### Visualizations Suggested
- [Chart type] for [purpose]
```

**Step 5.2: Automated Insights**

```python
insights = []

# Distribution insights
for col in numeric_columns:
    skew = df[col].skew()
    if abs(skew) > 1:
        insights.append({
            'type': 'distribution',
            'column': col,
            'finding': f'{col} is highly skewed ({skew:.2f})',
            'recommendation': 'Consider log transformation for analysis'
        })

# Missing value insights
for col in df.columns:
    missing_pct = df[col].isna().mean() * 100
    if missing_pct > 20:
        insights.append({
            'type': 'quality',
            'column': col,
            'finding': f'{col} has {missing_pct:.1f}% missing values',
            'recommendation': 'Investigate cause; consider imputation or exclusion'
        })

# Correlation insights
for (col1, col2), corr in strong_correlations:
    insights.append({
        'type': 'relationship',
        'columns': (col1, col2),
        'finding': f'Strong correlation ({corr:.2f}) between {col1} and {col2}',
        'recommendation': 'Consider multicollinearity in modeling'
    })
```

---

### Phase 6: Visualization Recommendations

**Chart Selection Guide:**

| Data Type | Question | Recommended Chart |
|-----------|----------|-------------------|
| Single numeric | Distribution? | Histogram, Box plot |
| Single categorical | Frequency? | Bar chart, Pie chart |
| Numeric vs Numeric | Relationship? | Scatter plot |
| Numeric vs Categorical | Comparison? | Box plot, Violin plot |
| Time series | Trend? | Line chart |
| Multiple categories | Composition? | Stacked bar, Treemap |
| Correlation matrix | Relationships? | Heatmap |

**Visualization Code Templates:**

```python
import matplotlib.pyplot as plt
import seaborn as sns

# Distribution
fig, ax = plt.subplots(figsize=(10, 6))
sns.histplot(df[column], kde=True, ax=ax)
ax.set_title(f'Distribution of {column}')

# Correlation heatmap
fig, ax = plt.subplots(figsize=(12, 8))
sns.heatmap(df.corr(), annot=True, cmap='coolwarm', center=0, ax=ax)
ax.set_title('Correlation Matrix')

# Time series
fig, ax = plt.subplots(figsize=(12, 6))
ax.plot(df['date'], df['value'])
ax.set_xlabel('Date')
ax.set_ylabel('Value')
ax.set_title('Value Over Time')

# Categorical comparison
fig, ax = plt.subplots(figsize=(10, 6))
sns.boxplot(x='category', y='value', data=df, ax=ax)
ax.set_title('Value by Category')
```

---

### Phase 7: Data Transformation Recommendations

**Common Transformations:**

```python
# Handle missing values
df[col].fillna(df[col].median())  # Numeric
df[col].fillna(df[col].mode()[0])  # Categorical
df[col].fillna(method='ffill')  # Time series

# Handle outliers
df[col].clip(lower=lower_bound, upper=upper_bound)  # Cap outliers
df = df[~is_outlier]  # Remove outliers

# Normalize/standardize
from sklearn.preprocessing import StandardScaler, MinMaxScaler
df[col] = StandardScaler().fit_transform(df[[col]])  # Z-score
df[col] = MinMaxScaler().fit_transform(df[[col]])  # 0-1 range

# Handle skewness
import numpy as np
df[col] = np.log1p(df[col])  # Log transform
df[col] = np.sqrt(df[col])  # Square root transform

# Encode categories
df = pd.get_dummies(df, columns=['category'])  # One-hot encoding
df[col] = df[col].astype('category').cat.codes  # Label encoding
```

---

## Output Formats

### Summary Statistics Table

| Column | Type | Non-Null | Missing% | Unique | Mean | Median | Std |
|--------|------|----------|----------|--------|------|--------|-----|
| col1 | int64 | 1000 | 0% | 50 | 25.3 | 24 | 10.2 |
| col2 | object | 950 | 5% | 10 | - | - | - |

### Correlation Matrix

| | A | B | C |
|---|---|---|---|
| A | 1.00 | 0.85 | -0.23 |
| B | 0.85 | 1.00 | -0.15 |
| C | -0.23 | -0.15 | 1.00 |

### Key Metrics Dashboard

```
┌─────────────────────────────────────────┐
│ Dataset: sales_data.csv                 │
├─────────────────────────────────────────┤
│ Records: 10,543  │  Features: 15        │
│ Quality: 94%     │  Completeness: 97%   │
├─────────────────────────────────────────┤
│ Top Insights:                           │
│ • Revenue up 15% YoY                    │
│ • Strong correlation: spend ↔ revenue   │
│ • 3 outliers detected in Q4             │
└─────────────────────────────────────────┘
```

---

## Quality Checklist

### Analysis Completeness
- [ ] Data profiling complete
- [ ] Missing values analyzed
- [ ] Distributions examined
- [ ] Correlations calculated
- [ ] Outliers identified
- [ ] Patterns documented

### Report Quality
- [ ] Executive summary provided
- [ ] Key findings prioritized
- [ ] Evidence included for claims
- [ ] Actionable recommendations
- [ ] Visualization suggestions

---

## Integration with Other Skills

### With database-schema-designer:
- Analyze data before schema design
- Identify normalization opportunities

### With technical-writer:
- Generate analysis documentation
- Create data dictionaries

---

## Troubleshooting

### Large datasets slow
- Use chunked reading: `pd.read_csv(..., chunksize=10000)`
- Sample for exploration: `df.sample(n=10000)`
- Use dtypes optimization: specify dtypes on read

### Memory errors
- Read columns selectively: `usecols=['col1', 'col2']`
- Use categorical dtype for low-cardinality strings
- Process in chunks

### Mixed data types
- Check with `df[col].apply(type).value_counts()`
- Force type on read: `dtype={'col': str}`

---

## Version History

- v1.0.0 (2025-12-07): Initial release with exploratory analysis, statistical methods, pattern recognition, and insight generation
