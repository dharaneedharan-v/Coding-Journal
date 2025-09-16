# *what is a cursor:* 

*A cursor in SQL is a database object used to process data one row at a time, useful when row-by-row handling is needed instead of bulk processing. It temporarily stores data for operations like SELECT, UPDATE, or DELETE.*

- *Useful for applying custom logic, conditional operations, or step-by-step updates.*
- *Common in PL/SQL or T-SQL for tasks like loops, conditional logic, or complex procedures.*

## ***Why Use a Cursor?***

*Cursors should be used carefully as they are helpful in scenarios like:*

- *Performing conditional logic row-by-row.*
- *Looping through data to calculate or transform fields*
- *Iterating over result sets for conditional updates or transformations.*
- *Handling hierarchical or recursive data structures.*
- *Performing clean-up tasks that can not be done with a single SQL Query.*


#### *TYPES OF CURSOR  :* 

#### *1. *Implicit vs Explicit Cursors***

- ***Implicit Cursor***
    
    - *Created automatically by the database when you run a single `INSERT`, `UPDATE`, `DELETE`, or `SELECT INTO`.*
        
    - *You don’t declare or manage it yourself.*
        
    - *Example: In Oracle/PLSQL, every `SELECT INTO` statement automatically uses an implicit cursor.*

###  *Explicit Cursor :*

- *Declared and controlled by the developer.*
    
- *You explicitly: `DECLARE → OPEN → FETCH → CLOSE`.*
    
- *Example: SQL Server’s `DECLARE cursor_name CURSOR FOR SELECT ...`*

# *Cursor Lifecycle (Rule Order)*

*Think of it as *4 steps you must always follow:***

1. ***DECLARE the cursor with a SELECT.**
    
2. ***OPEN the cursor to run the query.**
    
3. ***FETCH rows from the cursor inside a loop.**
    
4. ***CLOSE (and optionally DEALLOCATE) the cursor.**

### *Minimal Example (Beginner-Friendly — SQL Server style)*

```mysql 
DECLARE @id INT, @name NVARCHAR(100); -- variable declaration... 

-- 1) Declare
DECLARE my_cursor CURSOR FOR
SELECT EmployeeID, Name FROM Employees;

-- 2) Open
OPEN my_cursor;

-- 3) Fetch and loop
FETCH NEXT FROM my_cursor INTO @id, @name;

WHILE @@FETCH_STATUS = 0  -- @@ FETCh_STATUS is a build in call  IMPORTANT...
BEGIN
    PRINT 'Employee: ' + CAST(@id AS NVARCHAR) + ' - ' + @name;

    FETCH NEXT FROM my_cursor INTO @id, @name;
END

-- 4) Close + Deallocate
CLOSE my_cursor;
DEALLOCATE my_cursor;

```


# *🔹 Advantages of Cursors*

1. ***Row-by-row processing***
    
    - *Can handle each row separately (like a loop in programming).*
        
    - *Useful when logic cannot be done in one `UPDATE` or `SELECT`.*
        
2. ***Good for complex business rules***
    
    - *Example: send an email per employee, apply conditional salary raise, call procedures per row.*
        
3. ***Simple to understand for beginners***
    
    - *Works like a `for loop` in programming.*
        
4. ***Useful in stored procedures***
    
    - *When you must process each record step by step inside the database.*
        

*---*

# *🔹 Disadvantages of Cursors*

1. ***Slow performance ⚠️**
    
    - *Works row-by-row (RBAR = “Row By Agonizing Row”) instead of set-based.*
        
    - *Databases are optimized for set operations, not loops.*
        
2. ***High resource usage***
    
    - *Holds memory, temporary storage, and sometimes locks.*
        
3. ***Not scalable***
    
    - *Works for small datasets, but for thousands/millions of rows it becomes very slow.*
        
4. ***Code complexity***
    
    - *Requires DECLARE, OPEN, FETCH, CLOSE — more boilerplate compared to simple SQL.*
        
5. ***Not portable***
    
    - *Syntax differs across SQL Server, Oracle, MySQL, PostgreSQL.*




*✅ *Advantages → Row-by-row, flexible, simple to code, good for complex rules.***  
***❌ Disadvantages → Slow, heavy on resources, not scalable, messy code, DB-specific syntax.***

*👉 Golden Rule:*  
***“Use cursors only when set-based SQL cannot do the job***



EXAMPLES : 

This cursor goes through each row of the Employees table one by one and prints the Name


```mysql 
DECLARE @name NVARCHAR(100);

-- 1. Declare cursor
DECLARE name_cursor CURSOR FOR
SELECT Name FROM Employees;

-- 2. Open cursor
OPEN name_cursor;

-- 3. Fetch first row
FETCH NEXT FROM name_cursor INTO @name;

-- 4. Loop
WHILE @@FETCH_STATUS = 0
BEGIN
    PRINT 'Employee: ' + @name;

    FETCH NEXT FROM name_cursor INTO @name;
END;

-- 5. Close and deallocate
CLOSE name_cursor;
DEALLOCATE name_cursor;

```