
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

