# Financial Dashboard

Procedure for Creating Financial Dashboard:
Firstly, load the excel file into the Power BI and then perform ETL process to clean the dataset and unpivot the date columns. Next create measures which gives insights from the data.
## The measures i have used are:

### To find the sum of values(income, expenses, savings)
Values = sum(FinData[Value])

### To find the sum of Savings
Total saving = CALCULATE(sum(FinData[Value]),FinData[Type]="Savings")

### To find the sum of Income
Total income = CALCULATE(sum(FinData[Value]),FinData[Type]="Income")

### To find the sum of Expenses
Total expense = CALCULATE(sum(FinData[Value]),FinData[Type]="Expense")

### To find savings percentage
Saving % = divide([Total saving],[Total income])

### To find expenses percentage
Expense % = divide([Total expense],[Total income])

### setting savings target so that to know whether we are reaching the target saving amount or not by compare the savings amount of every month to the target
savings target = 0.25

### To calculate last month income
Income LM = calculate([Total income],DATEADD(FinData[Date],-1,MONTH))

### To calculate percentage change in last month income to current month income
Income change MOM % = DIVIDE([Total income],[Income LM])

### To calculate the networth by months
Cummulative Net worth = CALCULATE([Total saving],FILTER(ALL(FinData[Date]),FinData[Date] <= MAX((FinData[Date]))))
