**a) Female Representation**

      1) ###Female Count =
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
      
      3) Female % =
                  [Female Count] / [Total Count]



   
**b) Opportunity Equity**

      1) Promotion % Female =
                  VAR prom_count =
                      CALCULATE (
                          COUNT ( PR_DIV_FACT_EMPLOYEE_MASTER[EMP_ID] ),
                          FILTER (
                              PR_DIV_FACT_EMPLOYEE_MASTER,
                              PR_DIV_FACT_EMPLOYEE_MASTER[LAST_PROMOTION_DATE] >= MIN ( DIM_DATE_TABLE[Date] )
                                  && PR_DIV_FACT_EMPLOYEE_MASTER[LAST_PROMOTION_DATE] <= MAX ( DIM_DATE_TABLE[Date] )
                                  && PR_DIV_FACT_EMPLOYEE_MASTER[Gender] = "Female"
                          )
                      )
                  VAR headcount =
                      (
                          CALCULATE (
                              COUNT ( PR_DIV_FACT_EMPLOYEE_MASTER[EMP_ID] ),
                              FILTER (
                                  PR_DIV_FACT_EMPLOYEE_MASTER,
                                  PR_DIV_FACT_EMPLOYEE_MASTER[DOJ] <= MIN ( DIM_DATE_TABLE[Date] )
                                      && (
                                          ISBLANK ( PR_DIV_FACT_EMPLOYEE_MASTER[EXIT_DATE] )
                                              || PR_DIV_FACT_EMPLOYEE_MASTER[EXIT_DATE] > MIN ( DIM_DATE_TABLE[Date] )
                                      )
                                      && PR_DIV_FACT_EMPLOYEE_MASTER[Gender] = "Female"
                              )
                          )
                              + CALCULATE (
                                  COUNT ( PR_DIV_FACT_EMPLOYEE_MASTER[EMP_ID] ),
                                  FILTER (
                                      PR_DIV_FACT_EMPLOYEE_MASTER,
                                      PR_DIV_FACT_EMPLOYEE_MASTER[DOJ] <= MAX ( DIM_DATE_TABLE[Date] )
                                          && (
                                              ISBLANK ( PR_DIV_FACT_EMPLOYEE_MASTER[EXIT_DATE] )
                                                  || PR_DIV_FACT_EMPLOYEE_MASTER[EXIT_DATE] > MAX ( DIM_DATE_TABLE[Date] )
                                          )
                                          && PR_DIV_FACT_EMPLOYEE_MASTER[Gender] = "Female"
                                  )
                              )
                      ) / 2
                  RETURN
                      DIVIDE ( prom_count, headcount, 0 )

            2) Promotion % Male =
                        VAR prom_count =
                            CALCULATE (
                                COUNT ( PR_DIV_FACT_EMPLOYEE_MASTER[EMP_ID] ),
                                FILTER (
                                    PR_DIV_FACT_EMPLOYEE_MASTER,
                                    PR_DIV_FACT_EMPLOYEE_MASTER[LAST_PROMOTION_DATE] >= MIN ( DIM_DATE_TABLE[Date] )
                                        && PR_DIV_FACT_EMPLOYEE_MASTER[LAST_PROMOTION_DATE] <= MAX ( DIM_DATE_TABLE[Date] )
                                        && PR_DIV_FACT_EMPLOYEE_MASTER[Gender] = "Male"
                                )
                            )
                        VAR headcount =
                            (
                                CALCULATE (
                                    COUNT ( PR_DIV_FACT_EMPLOYEE_MASTER[EMP_ID] ),
                                    FILTER (
                                        PR_DIV_FACT_EMPLOYEE_MASTER,
                                        PR_DIV_FACT_EMPLOYEE_MASTER[DOJ] <= MIN ( DIM_DATE_TABLE[Date] )
                                            && (
                                                ISBLANK ( PR_DIV_FACT_EMPLOYEE_MASTER[EXIT_DATE] )
                                                    || PR_DIV_FACT_EMPLOYEE_MASTER[EXIT_DATE] > MIN ( DIM_DATE_TABLE[Date] )
                                            )
                                            && PR_DIV_FACT_EMPLOYEE_MASTER[Gender] = "Male"
                                    )
                                )
                                    + CALCULATE (
                                        COUNT ( PR_DIV_FACT_EMPLOYEE_MASTER[EMP_ID] ),
                                        FILTER (
                                            PR_DIV_FACT_EMPLOYEE_MASTER,
                                            PR_DIV_FACT_EMPLOYEE_MASTER[DOJ] <= MAX ( DIM_DATE_TABLE[Date] )
                                                && (
                                                    ISBLANK ( PR_DIV_FACT_EMPLOYEE_MASTER[EXIT_DATE] )
                                                        || PR_DIV_FACT_EMPLOYEE_MASTER[EXIT_DATE] > MAX ( DIM_DATE_TABLE[Date] )
                                                )
                                                && PR_DIV_FACT_EMPLOYEE_MASTER[Gender] = "Male"
                                        )
                                    )
                            ) / 2
                        RETURN
                            DIVIDE ( prom_count, headcount, 0 )

            3) Promotion Gap = 
                        [Promotion % Male] - [Promotion % Female]



**c) Female Leadership**

**d) Attrition Bias**

**e) Pay Equity**

**f) DEI Scorecard**
