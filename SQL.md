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