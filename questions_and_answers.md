# HR-Analytics-SQL-
## Questions and Answers

**Employee Demographics**

**1.** What is the total number of employees

````sql
select count(emp_id) as total_employees -- total num of employees 
from hr_analytics
where attrition like 'No'
````
**Results:**
total_employees|
---------------|
1236|

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

**3.** Which gender earns more?

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

**1.** How happy are our employees?

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
work_life_balance_rating|satisfaction_level|total|
|-----------------|------------------|-----|
1| unsatisfied| 80|
2| slightly satisfied| 344|
3| satisfied| 896|
4| very satisfied| 153|

**2.** Is there any correlation between years worked and work-life balance levels?

````sql
select work_life_balance, round(avg(years_at_company),1) as avg_years 
from hr_analytics
group by 1
````
**Results:**
work_life_balance_rating|avg_years|
------------------------|---------|
1| 6.4|
2| 7.0|
3| 7.1|
4| 7.0|

**Employee Tenure** 

**1.** What is the average tenure for all employees by department?

````sql
select department,round(avg(years_at_company),2) as avg_working_years 
from hr_analytics
group by 1
order by 2 asc
````
**Results:**
department|avg_working_years|
----------|-----------------|
Research & Development| 6.86|
Human Resources| 7.24|
Sales| 7.28|

**2.** What is the distribution of employees by year?

````sql
select years_in_current_role_bracket, count(emp_id) as employee_count 
from hr_analytics
group by 1
order by 1 asc
````
**Results:**
years_in_current_role_bracket|employee_count|
-----------------------------|--------------|
0-3| 810|
4-6| 177|
7-9| 379|
10-12| 61|
13+| 46|

**Promotions** 

**1.** What is the average time length since a promotion?
````sql
select round(avg(years_since_last_promotion),1) as avg_year_since_last_promo 
from hr_analytics
````
**Results**
avg_year_since_last_promo|
-------------------------|
2.2|

**2.** What is the average time length since a promotion by rating?
````sql
SELECT performance_rating, round(avg(years_since_last_promotion),1) as avg_year_since_last_promo 
from hr_analytics
group by 1
order by 1
````
**Results**
performance_rating| avg_year_since_last_promo|
------------------|--------------------------|
3| 2.2|
4| 2.3|
