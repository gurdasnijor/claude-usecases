# Data Analysis Assistant

> Explore datasets, perform statistical analysis, and generate actionable insights

## Overview

The Data Analysis Assistant helps you understand and extract value from structured data. It performs exploratory analysis, statistical summaries, pattern recognition, and provides actionable recommendations.

## When to Use

- **Explore new datasets** - Understand structure and contents
- **Assess data quality** - Find missing values, outliers, issues
- **Statistical analysis** - Distributions, correlations, trends
- **Find patterns** - Anomalies, segments, relationships
- **Generate insights** - Actionable findings and recommendations

## Supported Formats

| Format | Extension | Notes |
|--------|-----------|-------|
| **CSV** | .csv | Primary format |
| **JSON** | .json | Records or nested |
| **Excel** | .xlsx | Via pandas |
| **Parquet** | .parquet | Columnar storage |

## Quick Example

**Request:**
```
Analyze this sales data and tell me what's interesting:
[paste data or file path]
```

**Output:**
```markdown
## Analysis Summary

**Dataset:** 10,543 records, 15 columns
**Quality Score:** 94%

### Key Findings

1. **Revenue Trend:** Up 15% YoY with seasonal peaks in Q4
2. **Strong Correlation:** Marketing spend ↔ Revenue (r=0.82)
3. **Outliers:** 3 anomalous transactions in December

### Recommendations
- Increase Q4 marketing budget based on ROI correlation
- Investigate December outliers for data quality
```

## Analysis Types

| Type | Purpose | Output |
|------|---------|--------|
| **Descriptive** | Summarize data | Mean, median, distribution |
| **Diagnostic** | Explain patterns | Correlations, segments |
| **Quality** | Assess issues | Missing, outliers, errors |
| **Exploratory** | Discover insights | Patterns, anomalies |

## Statistical Methods

- **Central Tendency:** Mean, median, mode
- **Dispersion:** Std dev, IQR, range
- **Distribution:** Skewness, kurtosis, normality tests
- **Relationship:** Correlation, regression
- **Comparison:** t-tests, ANOVA

## Visualization Recommendations

| Question | Chart Type |
|----------|------------|
| Distribution? | Histogram, box plot |
| Trend over time? | Line chart |
| Relationship? | Scatter plot |
| Comparison? | Bar chart, box plot |
| Composition? | Pie chart, stacked bar |

## Data Quality Metrics

- **Completeness** - % non-null values
- **Uniqueness** - % non-duplicate rows
- **Validity** - % values within constraints
- **Consistency** - Format uniformity

## Related Skills

- **database-schema-designer** - Design from analyzed data
- **technical-writer** - Document analysis findings

## Version

- **Current:** v1.0.0
- **Last Updated:** 2025-12-07
- **Author:** 360 Social Impact Studios
