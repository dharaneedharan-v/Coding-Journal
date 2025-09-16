
*View is a database object..*
*view is created over a sql query.* 
*it does not store any data* 

*view  is a virtual table === > it does not store the data..*

*While table store the data......*


### *📌 1. Purpose*

*At the top, it says:*

1. ***Security***
    
2. ***To simplify complex SQL queries***
    

*These are *main reasons for using Views in SQL:***

- *Security → Hide sensitive columns and only expose what’s necessary.*
    
- *Simplicity → Users query a pre-built view instead of writing complex joins.*




*Rules when using CREATE OR REPLACE"* 

*=> Cannot change column name*
*=> Cannot change data type* 
*=> Cannot change order of the column BUT At the end we can add it...* 


*If we want to change the name of the column of a view  means  By using the Alter command Same as the DDL Synatx Only.. It does not  change the Original Table Column Name.....*


*DROP view use todrop the view..*

*Once the view is created it will not update it when the Original Table is altered or New product is added.* 

*If we want to do it Means we want to add the CREATE or REPLACE VIEW.* 



*Views Can be update able , if it is a single view or A single Table..  only Otherwise it will through An Error..* 


*Cannot have  the distinct clause..*

*group by also cant be updateable...* 

*if query contains the  with clause cannot update  such view* 
*if it contains the window function it cannot be updated able.* 


*Inserting the data in the View : possible ,* 

*By using the With check ...* 

*We can limit The insertion ,* 


*-- WITH CHECK OPTION*

```mysql
-- WITH CHECK OPTION

create or replace view apple_products
as
SELECT * from tb_product_info where brand = 'Apple'
with check option;

insert into apple_products
values ('P22', 'Macbook air', 'Apple', 2500, null);

select * from tb_product_info;
select * from apple_products;
```

## *🔹 What is a View?*

- *A *view is a database object created over an SQL query.***
    
- *Acts like a *virtual table → does not store data.***
    
- *Only stores the *SQL query definition.***
    
- *In contrast, a *table stores data physically.***
    

*---*

## *🔹 Purpose of Views*

1. ***Security***
    
    - *Hide sensitive columns.*
        
    - *Give users restricted access.*
        
    - *Example: expose only `name, salary` but hide `ssn`.*
        
2. ***Simplicity***
    
    - *Encapsulates *complex queries.***
        
    - *Users just query the view instead of writing multiple joins/aggregations.*
        

*---*

## *🔹 Rules & Limitations*

### ***Using `CREATE OR REPLACE VIEW`***

- *❌ Cannot rename columns.*
    
- *❌ Cannot change column data type.*
    
- *❌ Cannot change order of columns.*
    
- *✅ You can *add extra columns at the end.***
    

*👉 To rename a column → Use `ALTER VIEW` (but this only changes the alias in the view, not in the base table).*

*---*

### ***Structural Limitations***

- *Once created, a view does *not auto-update if the base table structure changes (e.g., new column).***  
    ***→ Must use `CREATE OR REPLACE VIEW`.**
    
- *`DROP VIEW view_name;` → removes the view.*
    

*---*

### ***Updatability of Views***

*A view is *updatable only if:***

- *Based on *a single table.***
    
- *Does not contain:*
    
    - *`DISTINCT`*
        
    - *`GROUP BY`*
        
    - *Aggregate functions (`SUM, AVG, COUNT...`)*
        
    - *`WITH` clause (CTEs)*
        
    - *Window functions (`ROW_NUMBER(), RANK(), ...`).*
        

*If any of the above are used → ❌ View is *read-only.***

*---*

### ***Inserting Data via Views***

- *✅ You can `INSERT` into an updatable view.*
    
- *Use *`WITH CHECK OPTION` to enforce conditions during insert/update.***
    

*---*

## *🔹 Example*

*Create Table :* 

```mysql 
CREATE TABLE employees (
    emp_id   INT PRIMARY KEY,
    emp_name VARCHAR(50),
    dept     VARCHAR(20),
    salary   NUMERIC
);

```

### *1. Create a view*
```mysql 
CREATE VIEW vw_hr AS
SELECT emp_id, emp_name, dept
FROM employees
WHERE dept = 'HR'
WITH CHECK OPTION;

```
### *2. Insert into the view*
```mysql 
INSERT INTO vw_hr (emp_id, emp_name, dept)
VALUES (101, 'Ali', 'HR');   -- ✅ Allowed
INSERT INTO vw_hr (emp_id, emp_name, dept)
VALUES (102, 'Sara', 'IT');  -- ❌ Error (blocked by WITH CHECK OPTION)

```
## *🔹 Summary (Interview 1-Liners)*

- ***View = virtual table (stores query, not data).**
    
- ***Security & simplicity = main purposes.**
    
- ***CREATE OR REPLACE VIEW → cannot rename/change datatype/order.**
    
- ***Updatable only if simple (single table, no group/distinct/window).**


*===============================================================*


# *Materialized View in SQL*


  *Materialized View in SQL  is a database object , created over the sql query , Simialry to the view* 
## *🔹 What is a Materialized View?*

- *A *materialized view is a database object created over a SQL query.***
    
- *Unlike a normal view (virtual), it stores *both:***
    
    1. *The SQL query definition*
        
    2. *The *query result data (physically on disk)***
        

*---*

## *🔹 How It Improves Performance*

- *Querying a materialized view does *not re-run the base query each time.***
    
- *Instead, it returns the *precomputed stored results → much faster performance.***
    
- *Great for *complex or expensive queries (aggregations, joins, millions of rows).***
    

*---*

## *🔹 Difference: View vs. Materialized View*

|Feature|Normal View|Materialized View|
|---|---|---|
|Stores query definition|✅ Yes|✅ Yes|
|Stores query result data|❌ No|✅ Yes|
|Performance|Slower (recomputes query)|Faster (returns stored data)|
|Data freshness|Always up-to-date|Can become stale|
|Refresh needed|❌ No|✅ Yes (manual or scheduled)|

*---*

## *🔹 Refreshing a Materialized View*

- *Since it stores data, it *does not auto-update when base tables change.***

```mysql 
REFRESH MATERIALIZED VIEW view_name;
```

