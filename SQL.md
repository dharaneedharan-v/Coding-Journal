
## Syntax : 


#### Substring Syntax : 

```mysql 
SUBSTRING(string, start, How_Many_Characters_To_Take)

```

#### Negative Index is possible , Here Index Start from the 1... 



===============================================================

HINT : 

For the point after the 2digit means Use the Round 

```sql
ROUND(

  --  (COUNT(DISTINCT player_id) / # parameters 

   -- (SELECT COUNT(DISTINCT player_id) FROM Activity) # parameters 

    ), 2

)
```

For the Consecutive days : 

```sql
 DATE_SUB(event_date, INTERVAL 1 DAY))
```
 
 ```sql
 date_add(b.event_date, interval 1 day ) = a.event_date
```



## Finding the Date In the particular Range  :


## The SQL BETWEEN Operator

The `BETWEEN` operator selects values within a given range. The values can be numbers, text, or dates.

The `BETWEEN` operator is inclusive: begin and end values are included. 


Selects all products with a price between 10 and 20:

```mysql

SELECT * FROM Products  
WHERE Price BETWEEN 10 AND 20;
```

===============================================================
## Having VS Where : 
====================

## ****Having vs WHERE****

| Having                                                              | Where                                                                   |
| ------------------------------------------------------------------- | ----------------------------------------------------------------------- |
| In the HAVING clause it will check the condition in group of a row. | In the WHERE condition it will check or execute at each row individual. |
| HAVING clause can only be used with aggregate function.             | The WHERE Clause cannot be used with aggregate function like Having     |
| Priority Wise HAVING Clause is executed after Group By.             | Priority Wise WHERE is executed before  Group By.                       |


- Cannot be used without `GROUP BY` unless an aggregate function is present.
- Must be placed after the `GROUP BY` clause and before the [`ORDER BY`](https://www.geeksforgeeks.org/sql-order-by/)clause (if used).

===============================================================

--------------
------------
--------


### [1068. Product Sales Analysis I](https://leetcode.com/problems/product-sales-analysis-i/)

```mysql
  

SELECT Product.product_name, Sales.year, Sales.price

FROM Sales

JOIN Product ON Sales.product_id = Product.product_id;

```


### [1378. Replace Employee ID With The Unique Identifier](https://leetcode.com/problems/replace-employee-id-with-the-unique-identifier/)

```mysql


select  EmployeeUNI.unique_id ,Employees.name

from  Employees

left join EmployeeUNI on  Employees.id = EmployeeUNI.id ;
```


### [197. Rising Temperature](https://leetcode.com/problems/rising-temperature/)

Logic :  create a another table and start compare with that from the start 1 and 0 in the table 1 
table 1     table 2 
day 1        day 1 
day 2        day 2 
	*HINT* [table1.day 1 =>  table2.day2 ]
	
	

```sql

SELECT a.id

FROM weather a

JOIN weather b

ON DATEDIFF(a.recordDate, b.recordDate) = 1 --

WHERE a.temperature > b.temperature;
```


### [1581. Customer Who Visited but Did Not Make Any Transactions](https://leetcode.com/problems/customer-who-visited-but-did-not-make-any-transactions/)


```Mysql
  

SELECT customer_id  , count(*) as count_no_trans -- Alias for the count does not need the customer_id again

FROM Visits

WHERE visit_id NOT IN (SELECT visit_id FROM Transactions)

group by customer_id;

```

### [1661. Average Time of Process per Machine](https://leetcode.com/problems/average-time-of-process-per-machine/)

```mysql
# Write your MySQL query statement below

select  machine_id , round(

    avg(case when activity_type = "end" then timestamp else null end )   -

    avg (case when activity_type = "start " then timestamp else null end ),

    3)

    as processing_time

    from  Activity

group by machine_id;
```


Using the  joins 

```mysql 
SELECT a.machine_id,

       ROUND(AVG(b.timestamp - a.timestamp), 3) AS processing_time

FROM activity a

JOIN activity b

ON a.process_id = b.process_id

AND a.machine_id = b.machine_id  

AND a.activity_type = 'start'

AND b.activity_type = 'end'

GROUP BY a.machine_id;

```

### [577. Employee Bonus](https://leetcode.com/problems/employee-bonus/)

```mysql 
# Write your MySQL query statement below

select e.name , b.bonus from employee e   left join bonus b

on e.empId = b.empId

where  bonus < 1000  or bonus is null  ;


```


### [570. Managers with at Least 5 Direct Reports](https://leetcode.com/problems/managers-with-at-least-5-direct-reports/)

```mysql 
SELECT e1.name

FROM employee e1

JOIN employee e2 ON e1.id = e2.managerId

GROUP BY e1.id

HAVING COUNT(e2.id) >=5;
```



### [620. Not Boring Movies](https://leetcode.com/problems/not-boring-movies/)

```sql


select * from Cinema

 where description !=  'boring' and id % 2 = 1

 order by  rating desc;
```


### [1075. Project Employees I](https://leetcode.com/problems/project-employees-i/)


 
```Mysql
select project_id , round(avg(experience_years * 1.0),2) as average_years 
from Project p 
join 
Employee  e 
on 
p.employee_id = e.employee_id
group by  project_id;

```


### [1633. Percentage of Users Attended a Contest](https://leetcode.com/problems/percentage-of-users-attended-a-contest/)

```mysql 

select r.contest_id , round( count(distinct u.user_id)/(select count(user_id) from Users ) * 100 ,2)   as percentage

 from Users u

inner join  Register r

on

u.user_id = r.user_id

group by r.contest_id

order by percentage desc, contest_id 

;
```


### [1211. Queries Quality and Percentage](https://leetcode.com/problems/queries-quality-and-percentage/)


```mysql
SELECT

    query_name,

    ROUND(AVG(rating / position), 2) AS quality,

    ROUND(AVG(rating < 3) * 100, 2) AS poor_query_percentage

FROM

    Queries

GROUP BY

    query_name ; 
```


### [1193. Monthly Transactions I](https://leetcode.com/problems/monthly-transactions-i/)

```mysql 
select

    date_format(trans_date , '%Y-%m') as month, # captial y for the Full Year small y for the 2 digit alone.

    country ,

    count( distinct id) as trans_count ,

    sum( case when state = 'approved' then 1 else 0 end) as  approved_count,

    sum(amount) as trans_total_amount ,

    sum(case when state = 'approved' then amount else 0 end ) as approved_total_amount

 from Transactions

 group by  date_format(trans_date , '%Y-%m') , country ;
```

### [1174. Immediate Food Delivery II](https://leetcode.com/problems/immediate-food-delivery-ii/)


```mysql
select round(sum(case when order_date = customer_pref_delivery_date then 1 else 0 end ) / count( distinct  customer_id) * 100 , 2 )   as  immediate_percentage

from Delivery

where (customer_id , order_date) in (

    select customer_id , min(order_date)

    from Delivery

    group by customer_id

)
;
```


### [3220. Odd and Even Transactions](https://leetcode.com/problems/odd-and-even-transactions/)


```mysql 
# Write your MySQL query statement below
select  transaction_date  , 
sum(case when amount % 2 = 1 then amount else 0 end ) as odd_sum , 
sum(case when amount % 2 = 0 then amount else 0 end ) as even_sum  
 from transactions 

group by transaction_date
order by transaction_date
;


```



### [2356. Number of Unique Subjects Taught by Each Teacher](https://leetcode.com/problems/number-of-unique-subjects-taught-by-each-teacher/)


```mysql
# Write your MySQL query statement below

select teacher_id   , count(distinct(subject_id)) as cnt from  Teacher

group by teacher_id

;
```


### [1141. User Activity for the Past 30 Days I](https://leetcode.com/problems/user-activity-for-the-past-30-days-i/) 


```mysql
# Write your MySQL query statement below

select activity_date as day  ,  count(distinct (user_id ))  as  active_users

from Activity where  activity_date between '2019-06-28' and '2019-07-27'

group by  activity_date ;
```
### [1070. Product Sales Analysis III](https://leetcode.com/problems/product-sales-analysis-iii/)

```mysql
# Write your MySQL query statement below

select (product_id) , year as first_year , quantity  , price  

from Sales where(product_id , year  ) in (select product_id  , min(year) from Sales group by product_id )

;
```


### [596. Classes With at Least 5 Students](https://leetcode.com/problems/classes-with-at-least-5-students/)


Think , The operation is to be performed Over all the group of rows, Not on the Single Row....
So We can use the Having ....
```mysql 
# Write your MySQL query statement below
select class  from Courses  group by class having count(*)>= 5  ; 
```


### [1729. Find Followers Count](https://leetcode.com/problems/find-followers-count/)

```mysql
# Write your MySQL query statement below

select user_id ,count(follower_id) as followers_count

from Followers

group by user_id  

order by user_id asc ;
```



### [619. Biggest Single Number](https://leetcode.com/problems/biggest-single-number/)


### 📌 Think of it like this:

Imagine you made a list of unique numbers on a piece of paper — if someone asks, _“What is this paper called?”_ you have to give it a name so you both know what you’re talking about.


Hint : After performing the It Subquery , The Temp  Results are Left  As Unused One We Want to Tell It or Give the Name for That operation... 

Because the database treats the subquery like a temporary table. Every table in SQL must have a name, and the subquery result is no exception — `unique_nums` is just that name 


```mysql
# Write your MySQL query statement below

    select max(num) as num  from

    (

        select num from MyNumbers

        group by num

        having count(num) = 1

    ) as dd

     ;
```



### [1045. Customers Who Bought All Products](https://leetcode.com/problems/customers-who-bought-all-products/)



```mysql 
select customer_id from Customer

group by customer_id

having (count(distinct (product_key))) = (select count(distinct(product_key)) from Product )
```

### [610. Triangle Judgement](https://leetcode.com/problems/triangle-judgement/)


```mysql 
# Write your MySQL query statement below
select x ,  y , z  ,  
case
when 
(x+y > z and y+ z > x and z + x > y ) then 'Yes'
else 'No'
end  as triangle
from Triangle ;

```


### [180. Consecutive Numbers](https://leetcode.com/problems/consecutive-numbers/) 

```mysql 
# Write your MySQL query statement below
-- select * , 
-- lead(num , 1) over(order by id)  as Lead1,
-- lead(num , 2 ) over(order by id)  as Lead2 
-- from Logs;

with cte as(
    select *  , 
lead(num , 1) over(order by id)  as Lead1,
lead(num , 2 ) over(order by id)  as Lead2 
from Logs
) 

Select distinct  num   as ConsecutiveNums
from cte where num  = lead1  and num = lead2 
 ;



```


### [1204. Last Person to Fit in the Bus](https://leetcode.com/problems/last-person-to-fit-in-the-bus/)


```mysql
# Write your MySQL query statement below

with CTE as(select turn , person_id , person_name , weight  , sum(weight) over(order by turn  ) as RunningSum
from Queue order by turn) 

select person_name from CTE  where RunningSum <= 1000 order by  RunningSum  desc limit 1   ;

```