# Customer_churn_analysis
In this project I used a dataset of multiple countries to analyze the churn rate of a busiess.

I used some measures to calculate the numbers, like :
TotalCustomers = CALCULATE(DISTINCTCOUNT(data[CustomerID]))
AvgTransPerCust = SUM(data[BasketPrice])/[TotalCustomers]

churn customers = 
VAR StartDate = DATE(2010, 12, 1) 
VAR EndDate = DATE(2011, 9, 9)  

VAR InitialPeriodCustomers = 
    CALCULATETABLE(
        VALUES(LatestTransactionByCustomer[CustomerID]),
        FILTER(
            data,
            data[InvoiceDate] >= StartDate &&
            data[InvoiceDate] <= EndDate
        )
    )

VAR SubsequentPeriodCustomers = 
    CALCULATETABLE(
        VALUES(LatestTransactionByCustomer[CustomerID]),
        FILTER(
            data,
            data[InvoiceDate] > EndDate &&
            data[InvoiceDate] <= EndDate +91
        )
    )
VAR ChurnedCustomers = EXCEPT(InitialPeriodCustomers, SubsequentPeriodCustomers)

RETURN
COUNTROWS(ChurnedCustomers)


Churn Rate = 
VAR StartDate = DATE(2010, 12, 1) 
VAR EndDate = DATE(2011, 9, 9)  

VAR InitialPeriodCustomers = 
    CALCULATETABLE(
        VALUES(data[CustomerID]),
        FILTER(
            data,
            data[InvoiceDate] >= StartDate &&
            data[InvoiceDate] <= EndDate
        )
    )

VAR SubsequentPeriodCustomers = 
    CALCULATETABLE(
        VALUES(data[CustomerID]),
        FILTER(
            data,
            data[InvoiceDate] > EndDate &&
            data[InvoiceDate] <= EndDate + 91
        )
    )

VAR ChurnedCustomers = EXCEPT(InitialPeriodCustomers, SubsequentPeriodCustomers)

RETURN
DIVIDE(COUNTROWS(ChurnedCustomers), COUNTROWS(InitialPeriodCustomers), 0)


Retention Rate = 
VAR StartDate = DATE(2010,12,1)  
VAR EndDate = DATE(2011, 09, 9)   

VAR InitialPeriodCustomers = 
    CALCULATETABLE(
        VALUES(data[CustomerID]),
        FILTER(
            data,
            data[InvoiceDate] >= StartDate &&
            data[InvoiceDate] <= EndDate
        )
    )

VAR SubsequentPeriodCustomers = 
    CALCULATETABLE(
        VALUES(data[CustomerID]),
        FILTER(
            data,
            data[InvoiceDate] > EndDate &&
            data[InvoiceDate] <= EndDate + 91
        )
    )

VAR RetainedCustomers = INTERSECT(InitialPeriodCustomers, SubsequentPeriodCustomers)

RETURN
DIVIDE(COUNTROWS(RetainedCustomers), COUNTROWS(InitialPeriodCustomers), 0)


TotalTransByChurnedCust = CALCULATE(SUM(LatestTransactionByCustomer[TotalSpend]),FILTER(LatestTransactionByCustomer,LatestTransactionByCustomer[ifBeforeDate]="Churned"))

Apart from these measures I used some chart and cards to visualize the data.





