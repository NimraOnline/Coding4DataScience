# Easy Level


### Workers With The Highest Salaries
> You have been asked to find the job titles of the highest-paid employees.
> Your output should include the highest-paid title or multiple titles with the same salary.

[Problem](https://platform.stratascratch.com/coding/10353-workers-with-the-highest-salaries?code_type=2)

```python
# Import your libraries
import pandas as pd

#Find highest salary value
max_salary = (max(worker['salary']))

#Find Worker IDs where the salary is >= max & dropna
worker_ids = worker['worker_id'].where(worker['salary'] >= max_salary)
worker_ids = worker_ids.dropna()

#Create a column where ID if max(salary) or 0
title['temp_ids'] = title['worker_ref_id'].apply(lambda x: x if x in list(worker_ids) else 0)

#Create series ignoring all 0 values & dropna 
output = title['worker_title'].where(title['temp_ids'] > 0)
output = output.dropna()

#Create dataframe with proper column name
df = pd.DataFrame({"best_paid_title": output})
return(df)
```

### Salaries Differences
> Write a query that calculates the difference between the highest salaries found in the marketing and engineering departments. Output just the absolute difference in salaries in a data frame.

[Problem](https://platform.stratascratch.com/coding/10308-salaries-differences?code_type=2)

```Python
# Import your libraries
import pandas as pd

# Start writing code
#1. Find the marketing ID 
marketing_id = int(db_dept['id'].where(db_dept['department']=='marketing').dropna())
#2. Find the engineering ID 
engineering_id = int(db_dept['id'].where(db_dept['department']=='engineering').dropna())

#3. Identify the max salary of all marketing IDs
highest_marketing = max(db_employee['salary'].where(db_employee['department_id'] == marketing_id).dropna())

#4. Identify the max salary of all engineering IDs
highest_eng = max(db_employee['salary'].where(db_employee['department_id'] == engineering_id).dropna())

#5. Calculate the absolute difference between both
diff_val = int(abs(highest_marketing - highest_eng))

df = pd.DataFrame({'sal_difference' : [diff_val]})
```




