a) Female Representation

      1) Female Count =
                        VAR Female_Count =
                            CALCULATE (
                                COUNT ( PR_DIV_FACT_EMPLOYEE_MASTER[Emp_ID] ),
                                PR_DIV_FACT_EMPLOYEE_MASTER[Active] = "Y"
                                    && PR_DIV_FACT_EMPLOYEE_MASTER[Gender] = "Female"
                            )
                        RETURN
                            Female_Count
      
      2) Total Count = 
              (
                  CALCULATE( countrows(PR_DIV_FACT_EMPLOYEE_MASTER),
                  PR_DIV_FACT_EMPLOYEE_MASTER[DOJ] <= date(year(today()),01,01),
                  (PR_DIV_FACT_EMPLOYEE_MASTER[EXIT_DATE] >= date(year(today()),01,01) || ISBLANK(PR_DIV_FACT_EMPLOYEE_MASTER[EXIT_DATE])) )
                  +
                          CALCULATE( countrows(PR_DIV_FACT_EMPLOYEE_MASTER),
                  PR_DIV_FACT_EMPLOYEE_MASTER[DOJ] <= max(DIM_DATE_TABLE[Date]),
                  (PR_DIV_FACT_EMPLOYEE_MASTER[EXIT_DATE] >= max(DIM_DATE_TABLE[Date]) || ISBLANK(PR_DIV_FACT_EMPLOYEE_MASTER[EXIT_DATE])) )
      
              ) /2
      
      3) 



    return Female_Count

b) Opportunity Equity

c) Female Leadership

d) Attrition Bias

e) Pay Equity

f) DEI Scorecard
