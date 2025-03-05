
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

