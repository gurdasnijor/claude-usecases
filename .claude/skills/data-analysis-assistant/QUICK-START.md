# Data Analysis Assistant - Quick Start

## Request Analysis

```
Analyze this data:
[paste CSV/JSON or describe dataset]

Focus on: [quality/trends/correlations/all]
```

---

## Quick Data Profile

```python
import pandas as pd
df = pd.read_csv('data.csv')

# Overview
print(f"Shape: {df.shape}")
print(f"Columns: {df.columns.tolist()}")
print(f"Types:\n{df.dtypes}")

# Stats
df.describe()

# Missing
df.isna().sum()
```

---

## Key Statistics

| Statistic | Code |
|-----------|------|
| Mean | `df[col].mean()` |
| Median | `df[col].median()` |
| Std Dev | `df[col].std()` |
| Correlation | `df.corr()` |
| Value counts | `df[col].value_counts()` |

---

## Data Quality Checks

```python
# Missing values
df.isna().sum()

# Duplicates
df.duplicated().sum()

# Outliers (IQR)
Q1, Q3 = df[col].quantile([0.25, 0.75])
IQR = Q3 - Q1
outliers = df[(df[col] < Q1-1.5*IQR) | (df[col] > Q3+1.5*IQR)]
```

---

## Analysis Checklist

- [ ] Shape and columns
- [ ] Data types
- [ ] Missing values
- [ ] Duplicates
- [ ] Distributions
- [ ] Outliers
- [ ] Correlations
- [ ] Trends (if time series)

---

## Chart Selection

| Data | Chart |
|------|-------|
| Single numeric | Histogram |
| Compare groups | Box plot |
| Time series | Line chart |
| 2 numeric vars | Scatter plot |
| Categories | Bar chart |

---

## Common Findings

| Finding | What to Look For |
|---------|------------------|
| Skewed distribution | Mean ≠ Median |
| Outliers | Points > 1.5×IQR |
| Strong correlation | r > 0.7 or r < -0.7 |
| Missing pattern | Non-random nulls |
| Trend | Consistent direction over time |

---

## Report Template

```markdown
## Summary
[1-2 sentences]

## Key Findings
1. [Finding with evidence]
2. [Finding with evidence]

## Data Quality
- Missing: [%]
- Outliers: [count]

## Recommendations
1. [Action]
```
