# Data Analysis Expressions used in the Project

## **a) Female Representation**

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
      
      3) Female % =
                  [Female Count] / [Total Count]



   
## **b) Opportunity Equity**

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



## **c) Female Leadership**

            1) Female Leader Count =
                              CALCULATE (
                                  COUNT ( PR_DIV_FACT_EMPLOYEE_MASTER[Emp_ID] ),
                                  PR_DIV_FACT_EMPLOYEE_MASTER[Active] = "Y"
                                      && PR_DIV_FACT_EMPLOYEE_MASTER[Level] = "Leadership"
                                      && PR_DIV_FACT_EMPLOYEE_MASTER[Gender] = "Female"
                              )


            2) Female Count =
                        VAR Female_Count =
                            CALCULATE (
                                COUNT ( PR_DIV_FACT_EMPLOYEE_MASTER[Emp_ID] ),
                                PR_DIV_FACT_EMPLOYEE_MASTER[Active] = "Y"
                                    && PR_DIV_FACT_EMPLOYEE_MASTER[Gender] = "Female"
                            )
                        RETURN
                            Female_Count

            3) Female Leadership % = 
                              [Female Leader Count] / [Female Count]

## **d) Attrition Bias**

            1) Attrition Rate Male =
                        VAR attrition_count =
                            CALCULATE (
                                COUNT ( PR_DIV_FACT_EMPLOYEE_MASTER[EMP_ID] ),
                                FILTER (
                                    PR_DIV_FACT_EMPLOYEE_MASTER,
                                    PR_DIV_FACT_EMPLOYEE_MASTER[EXIT_DATE] >= MIN ( DIM_DATE_TABLE[Date] )
                                        && PR_DIV_FACT_EMPLOYEE_MASTER[EXIT_DATE] <= MAX ( DIM_DATE_TABLE[Date] )
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
                            DIVIDE ( attrition_count, headcount, 0 )


            2) Attrition Rate Female =
                        VAR attrition_count =
                            CALCULATE (
                                COUNT ( PR_DIV_FACT_EMPLOYEE_MASTER[EMP_ID] ),
                                FILTER (
                                    PR_DIV_FACT_EMPLOYEE_MASTER,
                                    PR_DIV_FACT_EMPLOYEE_MASTER[EXIT_DATE] >= MIN ( DIM_DATE_TABLE[Date] )
                                        && PR_DIV_FACT_EMPLOYEE_MASTER[EXIT_DATE] <= MAX ( DIM_DATE_TABLE[Date] )
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
                            DIVIDE ( attrition_count, headcount, 0 )


            3) Attrition Gap = 
                        [Attrition Rate Female] - [Attrition Rate Male]



## **e) Pay Equity**

            1) Avg Pay Male =
                        CALCULATE (
                            AVERAGE ( PR_DIV_FACT_EMPLOYEE_MASTER[SALARY] ),
                            PR_DIV_FACT_EMPLOYEE_MASTER[Gender] = "Male",
                            PR_DIV_FACT_EMPLOYEE_MASTER[Active] = "Y"
                        )

            2) Avg Pay Female =
                        CALCULATE (
                            AVERAGE ( PR_DIV_FACT_EMPLOYEE_MASTER[SALARY] ),
                            PR_DIV_FACT_EMPLOYEE_MASTER[Gender] = "Female",
                            PR_DIV_FACT_EMPLOYEE_MASTER[Active] = "Y"
                        )

            3) Pay Gap =
                        ( [Avg Pay Male] - [Avg Pay Female] ) / [Avg Pay Male]

## **f) DEI Scorecard**

            1) Representation Score =
                        MIN ( 1, [Female %] / 0.2 )


            2) Leadership Score = 
                        MIN ( 1, [Female Leadership %] / 0.1)
                        

            3) Promotion Equity Score =
                        MIN ( 1, DIVIDE ( [Promotion % Female], [Promotion % Male], 0 ) )
                        

            4) Mobility Equity Score =
                        MIN ( 1, DIVIDE ( [Mobility % Female], [Mobility % Male], 0 ) )
                        
         

            5) Attrition Equity Score = 
                        MAX ( 0, 1 - ABS([Attrition Gap]) )


            6) Pay Equity Score =
                        MAX ( 0, 1 - ABS([Pay Gap]) )


            7) Overall DEI Score =
                        0.2 * [Representation Score] + 0.25 * [Leadership Score] + .15 * [Promotion Equity Score] + .10 * [Mobility Equity Score] + .15 * [Attrition Equity Score] + .15 * [Pay Equity Score] 

