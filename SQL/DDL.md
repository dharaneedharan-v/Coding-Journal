
# ALTER  :

- **CREATE** → create objects
    
- **ALTER** → modify objects
    
- **DROP** → remove objects
    
- **TRUNCATE** → clear data (structure remains)
    
- **RENAME** → rename objects
	



#### HINTS  :
1) If we have the constraints on the column we cant able to change or rename the column First we need to drop it then we can proceed with that one.....


## 📌 List of DDL Commands in SQL

Here’s the **core DDL** you’ll encounter:

1. **CREATE**
    
    - Create database objects
    
    ```sql
    CREATE DATABASE mydb;
    CREATE TABLE Employee (EmpID INT PRIMARY KEY, Name VARCHAR(100));
    CREATE INDEX idx_name ON Employee(Name);
    
    ```
    
2. **ALTER**
    
    - Modify an existing object
    
    ```sql
    ALTER TABLE Employee ADD COLUMN Age INT;
    ALTER TABLE Employee MODIFY COLUMN Name VARCHAR(200);
    ALTER TABLE Employee RENAME COLUMN Age TO EmpAge;
    ALTER TABLE Employee DROP COLUMN EmpAge;
    
    ```


# 🔹 1. `MODIFY`

- **Purpose**: Change a column’s **datatype**, **nullability**, or **default**
    
- **Column name stays the same**
    
- Syntax:
    
    ```sql
    ALTER TABLE table_name
    MODIFY column_name new_datatype [NULL | NOT NULL] [DEFAULT value];
    
    ```
    

✅ Example:

```sql
ALTER TABLE dd MODIFY Age BIGINT NOT NULL;

```

👉 This changes `Age` column’s type to `BIGINT`, makes it `NOT NULL`, but keeps the name `Age`.

---

# 🔹 2. `CHANGE`

- **Purpose**: Change a column’s **name** _and/or_ its **datatype**
    
- **You must always repeat the datatype**
    
- Syntax:
    
    ```sql
    ALTER TABLE table_name
    CHANGE old_column_name new_column_name new_datatype;
    
    ```
    

✅ Example:

```sql
ALTER TABLE dd CHANGE Salary AnnualSalary INT;

```

👉 This renames `Salary` → `AnnualSalary` and keeps it `INT`.

(If you wanted, you could also change the datatype here.)

---

# 🔹 3. `RENAME COLUMN` (MySQL 8+ only)

- **Purpose**: Rename a column **only** (keep datatype unchanged)
    
- Much simpler than `CHANGE`
    
- Syntax:
    
    ```sql
    ALTER TABLE table_name
    RENAME COLUMN old_column_name TO new_column_name;
    
    ```
    

✅ Example:

```sql
ALTER TABLE dd RENAME COLUMN Age TO StudentAge;

```

👉 This just renames `Age` → `StudentAge`, nothing else.
# 📌 Quick Comparison

| Command         | Rename Column | Change Datatype | Repeat Datatype Needed? | MySQL Version |
| --------------- | ------------- | --------------- | ----------------------- | ------------- |
| `MODIFY`        | ❌ No          | ✅ Yes           | ✅ Yes                   | All versions  |
| `CHANGE`        | ✅ Yes         | ✅ Yes           | ✅ Yes (always required) | All versions  |
| `RENAME COLUMN` | ✅ Yes         | ❌ No            | ❌ No                    | MySQL 8+ only |
|                 |               |                 |                         |               |

***USE THE CHANGE  TO RENAME AND CHANGE THE DATATYPE ALSO...................***


- If you **only** want to change datatype/constraints → use **MODIFY** (simpler).
- If you also want to **RENAME  + DATATYPE **  → use **CHANGE**  IT IS MANDATORY TO MENTION THE DATATYPE OTHERWISE IT WILL THROW AN ERROR .


# ***📌 MySQL `CHANGE` Column Syntax***

```sql
ALTER TABLE table_name
CHANGE old_column_name new_column_name new_datatype_OR_SAME_DATA_TYPE  [constraints (NOT NULL UNIQUE , PRIMARY KEY )];

```


3. **DROP**
    
    - Permanently delete an object
    
    ```sql
    DROP TABLE Employee;
    DROP DATABASE mydb;
    DROP INDEX idx_name ON Employee;
    
    ```
    
4. **TRUNCATE**
    
    - Remove **all data** from a table but keep the structure
    
    ```sql
    TRUNCATE TABLE Employee;
    
    ```
    
5. **RENAME**
    
    - Change the name of a database object (varies by SQL dialect)
    
    ```sql
    ALTER TABLE Employee RENAME TO Staff;   -- MySQL, PostgreSQL
    
    ```
    

---

## 📌 Constraints (part of DDL)

Adding/removing constraints is also **DDL**:

- **PRIMARY KEY**
    
    ```sql
    ALTER TABLE Employee ADD CONSTRAINT pk_emp PRIMARY KEY (EmpID);
    ALTER TABLE Employee DROP PRIMARY KEY;
    
    ```
    
- **UNIQUE**
    
    ```sql
    ALTER TABLE Employee ADD CONSTRAINT uq_email UNIQUE (Email);
    ALTER TABLE Employee DROP INDEX uq_email;
    
    ```
    
- **FOREIGN KEY**
    
    ```sql
    ALTER TABLE Employee ADD CONSTRAINT fk_dept FOREIGN KEY (DeptID) REFERENCES Department(DeptID);
    ALTER TABLE Employee DROP FOREIGN KEY fk_dept;
    
    ```
    
- **CHECK**
    
    ```sql
    ALTER TABLE Employee ADD CONSTRAINT chk_age CHECK (Age >= 18);
    ALTER TABLE Employee DROP CHECK chk_age;
    
    ```
    
- **DEFAULT**
    
    ```sql
    ALTER TABLE Employee ALTER COLUMN Age SET DEFAULT 18;   -- PostgreSQL
    ALTER TABLE Employee ALTER C
    
    ```

### This commads is used to Tell what are the Constraints that are presend in the table.


```mysql
SHOW CREATE TABLE boys;
```

```mysql 
OUTPUT :

| Table | Create Table                                                             
| dd    | CREATE TABLE `dd` (
  `Name` varchar(20) DEFAULT NULL,
  `RollNumber` bigint DEFAULT NULL,
  `Age` int DEFAULT NULL,
  `Address` varchar(20) DEFAULT NULL,
  `Location` varchar(20) DEFAULT NULL,
  `Subject` varchar(20) DEFAULT 'CSB=S',
  `Course_Fee` decimal(10,2) DEFAULT NULL,
  `Salary` int DEFAULT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci |
 
 
```