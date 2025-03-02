
### [1068. Product Sales Analysis I](https://leetcode.com/problems/product-sales-analysis-i/)

```mysql
  

SELECT Product.product_name, Sales.year, Sales.price

FROM Sales

JOIN Product ON Sales.product_id = Product.product_id;

```

