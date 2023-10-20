# HR-Analytics-SQL-
## Questions and Answers

**Employee Demographics**

**1.** What is the total number of employees

````sql
select count(emp_id) as total_employees -- total num of employees 
from hr_analytics
````
**Results:**
total_employees|
---------------|
1473|

**2.** What is the gender distribution?

````sql
select count(emp_id) as total_employees -- total num of employees 
from hr_analytics
````
**Results:**
gender|percentage|
------|----------|
male  |39.99|
female|60.01|

**3.** What is the age distribution? 

````sql
select age_group, round((count(emp_id) * 100.0) / (select count(emp_id) from hr_analytics),2) 
FROM hr_analytics
group by 1
order by 1 asc
````
**Results:**
age_group|percentage|
---------|----------|
18-25|8.35|
26-35|41.21|
36-45|31.91|
46-55|15.34|
55+  |3.19|

**4.** What is the attrition distribution?

````sql
select attrition, round((count(emp_id) * 100.0) / (select count(emp_id) from hr_analytics),2) as percentage 
FROM hr_analytics
group by 1
````
**Results:**
attrition|percentage|
---------|----------|
No| 83.91|
Yes| 16.09|

**Salary Analysis** 

**1.** What is the average income within the organization?

````sql
select round(avg(monthly_income * 12),2) as avg_income 
from hr_analytics
````
**Results:**
avg_income|
----------|
78002.75|

**2.** What is the average income by department?

````sql
select department, round(avg(monthly_income * 12),2) as avg_income
from hr_analytics
group by 1
````
**Results:**
department|avg_income|
----------|----------|
Human Resources| 79854.10|
Research & Development| 75375.03|
Sales| 83402.87|

**3.** What is the average income by job level?

````sql
select job_level, round(avg(monthly_income * 12),2) as avg_income -- avg annual income by level
from hr_analytics
group by 1 
order by 1 asc 
````
**Results:**
job_level|avg_income|
----------|----------|
1| 33446.93|
2| 65961.58|
3| 117816.55|
4| 186045.40|
5| 230301.91|

**3.** What gender earns more?

````sql
select gender, round(avg(monthly_income * 12),2) as avg_income -
from hr_analytics
group by 1
````
**Results:**
job_level|avg_income|
----------|----------|
Female| 80162.99|
Male| 76563.39|

**Work-Life Balance** 

**1.** What are the satisfaction levels for all employees?

````sql
select work_life_balance,
	case 
    	when work_life_balance = 1 then 'unsatisfied' 
    	when work_life_balance = 2 then 'slightly satisfied' 
    	when work_life_balance = 3 then 'satisfied' 
    	else 'very satisfied'
	end as satisfaction_level,
count(emp_id) as total
from hr_analytics
group by 1
order by 1 asc
````
**Results:**
work_life_balance|satisfaction_level|total|
|-----------------|------------------|-----|
1| unsatisfied| 80|
2| slightly satisfied| 344|
3| satisfied| 896|
4| very satisfied| 153|

















