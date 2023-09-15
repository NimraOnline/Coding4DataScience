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




