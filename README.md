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
* Evaluate pay equity across comparable groups:
  
  Analyze salary differences between genders across grades, region, unit and job family to assess compensation fairness.
* Develop a composite DEI score for decision-making:
  
  Integrate multiple DEI dimensions into a single, standardized metric to track performance and guide strategic actions.

---

## Tools & Technology Used

Oracle SQl --> Power Query --> DAX --> Power BI

* **Oracle SQL** : Data storage & Data Extraction
* **Power Query** : Data Extraction, Data Transformation & Data Cleaning
* **Power BI** : Data Transformation, Data Modelling, Data Analysis & Data Visualization
* **DAX** : Aggregations, Metrics & Calculations
---

## Data Model

###  Fact Table

* `FACT_Employee_Master`

  * Emp_ID
  * Emp_Name
  * Gender
  * DOB
  * Date of Joining
  * Unit
  * Location
  * Region
  * Department
  * Role
  * Job Family
  * Cadre
  * Grade
  * Annual Salary
  * Exit Date
  * Last Promotion Date
  * Last Role Change Date
  * Last Location Change Date
  * Last Department Change Date

###  Dimension Tables

* DIM_Location_Master
  *  Location Code
  *  Location Name

* DIM_Role_Master
  *  Role ID
  *  Role Name
  
* DIM_Job_Master
  * Job ID
  * Job Family Name
  
* DIM_Unit_Master
  * Unit Code
  * Unit Name
    
* DIM_Grade_Master
  *  Grade Code
  *  Grade Name
  *  Cadre Code
  *  Cadre Name
  *  Management Level

---

## Key Metrics

### Workforce Representation

* Female Active Count as on Key Date
* Total Active Count as on Key Date
* Female Workforce % as on Key Date = Female count as on Key Date / Total Active Manpower as on Key Date
* Female Workforce % by Date/ Cadre/ Grade/ Unit/ Job Family
* Representation Equity Score = Actual Female Workforce % / Target Female Workforce %

---

### Opportunity Equity

* Gender wise Promotion Rate (5-year window) = Total Promotions in period / Average Manpower Count in period
* Promotion Gap = Male Promotion % - Female Promotion %
* Female Promotion % by Management Level (Leadership/ Middle Management/ Entry Level/ Support Staff)
* Gender wise Mobility Rate (Role/Location/Dept changes)
* Mobility Gap = Male Mobility % - Female Mobility %
* Promotion Equity Score = Female Promotion % / Male Promotion %
* Mobility Equity Score =  Female Mobility % / Male Mobility %

---

### Female Leadership

* Female Leader Count =  Active Females in Leadership Grades (E8 to E11)
* Female Leadership % = Female Leader Count / Active Manpower Count in Leadership Grades (E8 to E11)
* Female Leadership % by Date/ Leadership Grades (E8 to E11) / Region/ Job Family
* Leadership Equity Score = Actual Female Leadership % / Target Female Leadership %  

---

### Attrition Bias

* Gender wise Attrition Rate (5-year window) = Total Attritions in period / Average Manpower Count in period
* Attrition Gap % =  Female Attrition % - Male Attrition %
* Attrition Gap by Date/ Management Level/ Region/ Tenure Band/ Unit/ Job Family
* Attrition Equity Score = 1 - abs(Attrition Gap%)

---

### Pay Equity

* Gender wise Avg Salary = Sum of Salary as on Date / Total Active Manpower as on Date
* Pay Gap % = (Avg Male Salary - Avg Female Salary) / Avg Male Salary
* Pay Gap by Management Level/ Unit/ Job Family/ Region
* Pay Equity Score = 1 - abs(Pay Gap%)

---

## DEI Score Framework

DEI Score =
        (Representation Equiry Score * 20%) +
        (Leadership Equity Score * 25%) +
        (Attrition Equity Score * 15%) +
        (Pay Equity Score * 15%) +
        (Promotion Equity Score * 15%) +
        (Mobility Equity Score * 10%)

---

## Dashboard Pages

### 1. DEI Overview

* Filters: Date/ Region/ Unit/ Location/ Cadre/ Grade/ Job Family/ Role
* KPI:
* Visuals:
  
---

### 2. Female Representation

* Filters: Date/ Region/ Unit/ Location/ Cadre/ Grade/ Job Family/ Role
* KPI:
* Visuals:

---

### 3. Opportunity Equity

* Filters: Date/ Region/ Unit/ Location/ Cadre/ Grade/ Job Family/ Role
* KPI:
* Visuals:

---

### 4. Female Leadership

* Filters: Date/ Region/ Unit/ Location/ Cadre/ Grade/ Job Family/ Role
* KPI:
* Visuals:

---

### 5. Attrition Bias

* Filters: Date/ Region/ Unit/ Location/ Cadre/ Grade/ Job Family/ Role
* KPI:
* Visuals:

---

### 6. Pay Equity

* Filters: Date/ Region/ Unit/ Location/ Cadre/ Grade/ Job Family/ Role
* KPI:
* Visuals:

---

## Key Insights (Sample)

* Female representation declines significantly at senior levels
* Higher attrition observed among women in mid-career stages
* Promotion and mobility gaps contribute to leadership imbalance
* Technical functions show lower diversity levels

---

## Author

Asad Ali

