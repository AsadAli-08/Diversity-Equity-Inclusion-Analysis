# Diversity Equity & Inclusion Analysis

## Project Overview

Organizations today are increasingly focused on building diverse, equitable, and inclusive workplaces, yet many struggle to translate data into actionable insights. This project presents a comprehensive Diversity, Equity & Inclusion (DEI) Analytics Dashboard that goes beyond basic reporting to deliver a structured, data-driven decision framework.

Built using Power BI, SQL, and DAX, the solution integrates multiple dimensions like workforce data—representation, leadership diversity, attrition, pay, mobility and career progression—to provide a holistic view of DEI performance. It introduces a composite DEI score that consolidates these dimensions into a single, comparable metric, enabling leadership to quickly assess overall performance.

By highlighting gaps, identifying root causes, and prioritizing action areas, this project aims to empower HR and Top Management to move from reactive analysis to proactive decision-making.

---

## Project Objectives

* Measure workforce diversity and representation:
  
  Analyze gender distribution across grades, functions, roles, units, location and regions to identify gaps against defined DEI targets.
* Assess leadership pipeline and progression equity:
  
  Evaluate representation at senior levels and identify structural barriers in promotions and mobility.
* Identify attrition bias and retention risks:
  
  Detect disparities in attrition rates across gender, grade, region, unit, function, and tenure to uncover inclusion challenges.
* Evaluate opportunity equity in career progression:
  
  Analyze promotion and mobility equity by comparing rates across genders to identify disparities in access to growth opportunities.
* Evaluate pay equity across comparable groups
  Analyze salary differences between genders across grades, region, unit and job family to assess compensation fairness.
* Develop a composite DEI score for decision-making
  Integrate multiple DEI dimensions into a single, standardized metric to track performance and guide strategic actions.

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

