# Diversity Equity & Inclusion Analysis (Power BI + SQL + Python)

## Project Overview

This project builds a comprehensive Diversity, Equity & Inclusion (DEI) analytics solution designed for enterprise HR decision-making (with a PSU-focused context).

The solution goes beyond descriptive reporting and delivers a decision-support system by combining:

* Representation analysis
* Leadership pipeline tracking
* Attrition bias detection
* Pay equity evaluation
* Opportunity (promotion & mobility) equity
* DEI scorecard with actionable insights

---

## Key Objectives

* Measure workforce diversity across dimensions
* Identify structural gaps in leadership pipeline
* Detect attrition bias across gender and functions
* Evaluate fairness in compensation and career growth
* Provide a **composite DEI score** for executive decision-making
* Enable **data-driven HR interventions**

---

## Tools & Technology Used

* **Oracle SQL** → Data storage & Extraction
* **Power BI** → Data extraction, Transformation, Cleansing , Analysis & Visualization
* **DAX** → Advanced metrics & Measures

---

## Data Model

###  Fact Table

* `PR_DIV_FACT_EMPLOYEE_MASTER`

  * Employee attributes
  * Salary, performance
  * Promotion & movement dates
  * Exit information

---

## Key Metrics

### Representation

* Female Workforce %
* Female Representation by Grade / Region / Function

---

### Leadership Diversity

* Female Leadership % (E7+)
* Pipeline leakage across grades

---

### Attrition Bias

* Attrition Rate (Male vs Female)
* Attrition Gap %
* Attrition by Grade / Tenure / Region

---

### Pay Equity

* Avg Salary (Male vs Female)
* Pay Gap %

---

### Opportunity Equity

* Promotion Rate (5-year window)
* Mobility Rate (Role/Location/Dept changes)
* **Opportunity Score**

---

## DEI Score Framework

A composite index combining key dimensions:

```
DEI Score =
(Representation × 25%) +
(Leadership × 25%) +
(Attrition Equity × 15%) +
(Pay Equity × 15%) +
(Opportunity Equity × 20%)
```

---

## Equity Score Logic

| Component      | Formula           |
| -------------- | ----------------- |
| Representation | Actual / Target   |
| Leadership     | Actual / Target   |
| Attrition      | 1 - ABS(Gap)      |
| Pay            | 1 - ABS(Gap)      |
| Promotion      | Female % / Male % |
| Mobility       | Female % / Male % |

---

## Dashboard Pages

### 1. Executive Summary

* KPI overview
* Trend vs target
* Key risks
* Top action areas

---

### 2. DEI Overview

* Workforce representation
* Leadership diversity
* Gap vs target

---

### 3. Career Progression

* Pipeline analysis
* Promotion trends
* Mobility insights

---

### 4. Attrition Bias

* Gender-based attrition
* Grade / tenure analysis
* Department heatmap

---

### 5. Pay Equity

* Salary comparison
* Pay gap by grade & function
* Distribution analysis

---

### 6. DEI Scorecard

* Metrics vs targets
* Gap analysis
* RAG status indicators

---

## Key Insights (Sample)

* Female representation declines significantly at senior levels
* Higher attrition observed among women in mid-career stages
* Promotion and mobility gaps contribute to leadership imbalance
* Technical functions show lower diversity levels

---

## Author

Asad Ali

