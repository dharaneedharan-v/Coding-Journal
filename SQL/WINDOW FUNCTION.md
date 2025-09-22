# _What are Window Functions (RANK, DENSE_RANK, LEAD/LAG):_

_Window functions are SQL analytical functions that perform calculations across a set of table rows related to the current row. Unlike aggregate functions, they don't collapse rows into groups but return a value for each individual row based on a "window" of related data._

- _RANK() and DENSE_RANK() assign rankings to rows based on specified criteria._
- _LEAD() and LAG() access data from subsequent or previous rows without joins._
- _All use OVER() clause to define the window of data to operate on._
- _Essential for analytical queries, reporting, and data analysis tasks._

## _**Why Use Window Functions?**_

_Window functions are powerful because they allow you to:_

- _Rank employees by salary within each department without grouping._
- _Compare current row values with previous/next rows (time series analysis)._
- _Perform running totals, moving averages, and analytical calculations._
- _Avoid complex self-joins that would otherwise be needed._
- _Create sophisticated reports with rankings and comparisons in a single query._

---

# _🔹 RANK() Function_

_RANK() assigns a rank to each row within a partition, with gaps for tied values._

### _**Syntax:**_

```sql
RANK() OVER (
    [PARTITION BY column1, column2, ...]
    ORDER BY column1 [ASC|DESC], column2 [ASC|DESC], ...
)
```

### _**Key Characteristics:**_

- _Assigns same rank to tied values_
- _Leaves gaps after tied ranks (1, 2, 2, 4, 5...)_
- _PARTITION BY divides data into groups (optional)_
- _ORDER BY determines ranking criteria (required)_

### _**Example 1: Employee Salary Ranking**_

```sql
SELECT 
    employee_id,
    first_name,
    department,
    salary,
    RANK() OVER (ORDER BY salary DESC) AS overall_rank,
    RANK() OVER (PARTITION BY department ORDER BY salary DESC) AS dept_rank
FROM employees;
```

_Result:_

```
employee_id | first_name | department | salary | overall_rank | dept_rank
------------|------------|------------|--------|--------------|----------
101         | John       | IT         | 75000  | 1            | 1
102         | Sarah      | IT         | 70000  | 2            | 2
103         | Mike       | HR         | 70000  | 2            | 1
104         | Lisa       | HR         | 65000  | 4            | 2
105         | Tom        | IT         | 60000  | 5            | 3
```

---

# _🔹 DENSE_RANK() Function_

_DENSE_RANK() assigns ranks without gaps, even when there are ties._

### _**Syntax:**_

```sql
DENSE_RANK() OVER (
    [PARTITION BY column1, column2, ...]
    ORDER BY column1 [ASC|DESC], column2 [ASC|DESC], ...
)
```

### _**Key Characteristics:**_

- _Assigns same rank to tied values_
- _No gaps in ranking sequence (1, 2, 2, 3, 4...)_
- _Consecutive rankings regardless of ties_

### _**Example 2: Dense Ranking Comparison**_

```sql
SELECT 
    student_name,
    score,
    RANK() OVER (ORDER BY score DESC) AS rank_with_gaps,
    DENSE_RANK() OVER (ORDER BY score DESC) AS dense_rank_no_gaps
FROM exam_results
ORDER BY score DESC;
```

_Result:_

```
student_name | score | rank_with_gaps | dense_rank_no_gaps
-------------|-------|----------------|-------------------
Alice        | 95    | 1              | 1
Bob          | 90    | 2              | 2
Charlie      | 90    | 2              | 2
David        | 85    | 4              | 3  ← Notice: 3 vs 4
Eva          | 80    | 5              | 4
```

---

# _🔹 LAG() Function_

_LAG() accesses data from a previous row in the result set without using a self-join._

### _**Syntax:**_

```sql
LAG(column_name, offset, default_value) OVER (
    [PARTITION BY column1, column2, ...]
    ORDER BY column1 [ASC|DESC], column2 [ASC|DESC], ...
)
```

### _**Parameters:**_

- _column_name: Column to retrieve from previous row_
- _offset: Number of rows back (default = 1)_
- _default_value: Value when no previous row exists (optional)_

### _**Example 3: Sales Comparison with Previous Month**_

```sql
SELECT 
    month_year,
    sales_amount,
    LAG(sales_amount) OVER (ORDER BY month_year) AS previous_month_sales,
    LAG(sales_amount, 2) OVER (ORDER BY month_year) AS two_months_ago,
    sales_amount - LAG(sales_amount) OVER (ORDER BY month_year) AS month_over_month_change
FROM monthly_sales
ORDER BY month_year;
```

_Result:_

```
month_year | sales_amount | previous_month_sales | two_months_ago | month_over_month_change
-----------|--------------|---------------------|----------------|------------------------
2024-01    | 50000        | NULL                | NULL           | NULL
2024-02    | 55000        | 50000               | NULL           | 5000
2024-03    | 48000        | 55000               | 50000          | -7000
2024-04    | 62000        | 48000               | 55000          | 14000
```

---

# _🔹 LEAD() Function_

_LEAD() accesses data from a subsequent row in the result set._

### _**Syntax:**_

```sql
LEAD(column_name, offset, default_value) OVER (
    [PARTITION BY column1, column2, ...]
    ORDER BY column1 [ASC|DESC], column2 [ASC|DESC], ...
)
```

### _**Parameters:**_

- _column_name: Column to retrieve from next row_
- _offset: Number of rows forward (default = 1)_
- _default_value: Value when no next row exists (optional)_

### _**Example 4: Employee Career Progression**_

```sql
SELECT 
    employee_id,
    promotion_date,
    current_salary,
    LEAD(current_salary) OVER (
        PARTITION BY employee_id 
        ORDER BY promotion_date
    ) AS next_salary,
    LEAD(promotion_date) OVER (
        PARTITION BY employee_id 
        ORDER BY promotion_date
    ) AS next_promotion_date
FROM employee_promotions
ORDER BY employee_id, promotion_date;
```

---

# _🔹 Complex Real-World Examples_

### _**Example 5: Top N per Group with RANK**_

```sql
-- Get top 3 highest paid employees per department
WITH ranked_employees AS (
    SELECT 
        employee_id,
        first_name,
        department,
        salary,
        RANK() OVER (PARTITION BY department ORDER BY salary DESC) AS dept_rank
    FROM employees
)
SELECT *
FROM ranked_employees
WHERE dept_rank <= 3
ORDER BY department, dept_rank;
```

### _**Example 6: Running Comparison Analysis**_

```sql
-- Sales performance analysis with multiple window functions
SELECT 
    sales_date,
    daily_sales,
    -- Ranking
    RANK() OVER (ORDER BY daily_sales DESC) AS sales_rank,
    DENSE_RANK() OVER (ORDER BY daily_sales DESC) AS dense_sales_rank,
    
    -- Previous/Next day comparison
    LAG(daily_sales) OVER (ORDER BY sales_date) AS previous_day_sales,
    LEAD(daily_sales) OVER (ORDER BY sales_date) AS next_day_sales,
    
    -- Week-over-week comparison
    LAG(daily_sales, 7) OVER (ORDER BY sales_date) AS same_day_last_week,
    
    -- Percentage change
    ROUND(
        (daily_sales - LAG(daily_sales) OVER (ORDER BY sales_date)) * 100.0 / 
        LAG(daily_sales) OVER (ORDER BY sales_date), 2
    ) AS day_over_day_pct_change
    
FROM daily_sales_data
ORDER BY sales_date;
```

---

# _🔹 Common Use Cases_

### _**RANK/DENSE_RANK Use Cases:**_

- _Employee performance rankings_
- _Product sales rankings_
- _Student grade rankings_
- _Customer value segmentation_
- _Competition leaderboards_

### _**LAG/LEAD Use Cases:**_

- _Time series analysis (month-over-month growth)_
- _Sequential data comparison_
- _Trend analysis_
- _Gap analysis in data_
- _Customer journey analysis_

---

# _🔹 Advantages of Window Functions_

1. _**Eliminates Complex Self-Joins**_
    
    - _No need for complicated join syntax to compare rows._
    - _Cleaner, more readable code._
2. _**Better Performance**_
    
    - _More efficient than subqueries and self-joins._
    - _Database optimizers handle window functions well._
3. _**Analytical Power**_
    
    - _Enable sophisticated analysis in single queries._
    - _Perfect for reporting and business intelligence._
4. _**Flexible Partitioning**_
    
    - _Can group data logically without aggregating._
    - _Maintains row-level detail while adding analytical context._
5. _**Easy Ranking and Comparison**_
    
    - _Simple syntax for complex ranking requirements._
    - _Natural solution for top-N problems._

---

# _🔹 Disadvantages/Limitations_

1. _**Performance on Large Datasets**_
    
    - _Can be resource-intensive on very large tables._
    - _May require proper indexing on PARTITION BY and ORDER BY columns._
2. _**Memory Usage**_
    
    - _Window functions may need to sort large result sets in memory._
    - _Can cause performance issues without proper system resources._
3. _**Database Compatibility**_
    
    - _Not supported in all SQL databases (older versions)._
    - _Syntax variations between different database systems._
4. _**Learning Curve**_
    
    - _More complex than basic SQL for beginners._
    - _Requires understanding of OVER clause and partitioning concepts._
5. _**Limited Nesting**_
    
    - _Cannot nest window functions directly._
    - _May need CTEs or subqueries for complex scenarios._

---

# _🔹 Alternative Approaches_

### _**Instead of Window Functions (Traditional Approach):**_

#### _Old Way: Self-Join for Ranking_

```sql
-- ❌ Complex self-join approach
SELECT e1.employee_id, e1.salary,
       COUNT(e2.employee_id) + 1 AS rank
FROM employees e1
LEFT JOIN employees e2 ON e2.salary > e1.salary
GROUP BY e1.employee_id, e1.salary
ORDER BY rank;
```

#### _New Way: Window Function_

```sql
-- ✅ Simple window function
SELECT employee_id, salary,
       RANK() OVER (ORDER BY salary DESC) AS rank
FROM employees;
```

### _**Instead of LAG/LEAD: Self-Join with ROW_NUMBER**_

```sql
-- ❌ Complex approach
SELECT s1.month_year, s1.sales, s2.sales AS previous_month
FROM (SELECT *, ROW_NUMBER() OVER (ORDER BY month_year) AS rn 
      FROM sales) s1
LEFT JOIN (SELECT *, ROW_NUMBER() OVER (ORDER BY month_year) AS rn 
           FROM sales) s2 ON s1.rn = s2.rn + 1;

-- ✅ Simple LAG function
SELECT month_year, sales,
       LAG(sales) OVER (ORDER BY month_year) AS previous_month
FROM sales;
```

---

# _🔹 Performance Tips_

### _**Optimization Best Practices:**_

1. _**Index PARTITION BY and ORDER BY columns**_
    
    ```sql
    CREATE INDEX idx_emp_dept_salary ON employees (department, salary DESC);
    ```
    
2. _**Use appropriate PARTITION BY to reduce window size**_
    
    ```sql
    -- ✅ Better: Smaller partitions
    RANK() OVER (PARTITION BY department ORDER BY salary DESC)
    
    -- ❌ Slower: Large window
    RANK() OVER (ORDER BY salary DESC)
    ```
    
3. _**Filter before window functions when possible**_
    
    ```sql
    -- ✅ Filter first, then apply window function
    SELECT employee_id, salary,
           RANK() OVER (ORDER BY salary DESC) AS rank
    FROM employees
    WHERE active = 1 AND department = 'IT';
    ```
    

---

_**✅ Advantages → Eliminates complex joins, better performance, analytical power, flexible partitioning.**_  
_**❌ Disadvantages → Resource-intensive on large data, memory usage, compatibility issues, learning curve.**_



# 🔹 **Ranking Functions**

```sql
ROW_NUMBER() OVER (
    [PARTITION BY column]
    ORDER BY column ASC|DESC
)

RANK() OVER (
    [PARTITION BY column]
    ORDER BY column ASC|DESC
)

DENSE_RANK() OVER (
    [PARTITION BY column]
    ORDER BY column ASC|DESC
)

NTILE(n) OVER (
    [PARTITION BY column]
    ORDER BY column ASC|DESC
)   -- divides result into n equal buckets

```

---

# 🔹 **Aggregate Window Functions**

```sql
SUM(column) OVER (
    [PARTITION BY column]
    [ORDER BY column]
    [ROWS BETWEEN ...]
)

AVG(column) OVER (
    [PARTITION BY column]
    [ORDER BY column]
    [ROWS BETWEEN ...]
)

COUNT(column) OVER (
    [PARTITION BY column]
    [ORDER BY column]
    [ROWS BETWEEN ...]
)

MIN(column) OVER (
    [PARTITION BY column]
    [ORDER BY column]
)

MAX(column) OVER (
    [PARTITION BY column]
    [ORDER BY column]
)

```

---

# 🔹 **Navigation Functions**

```sql
LAG(column, offset, default) OVER (
    [PARTITION BY column]
    ORDER BY column
)

LEAD(column, offset, default) OVER (
    [PARTITION BY column]
    ORDER BY column
)

FIRST_VALUE(column) OVER (
    [PARTITION BY column]
    ORDER BY column
)

LAST_VALUE(column) OVER (
    [PARTITION BY column]
    ORDER BY column
    ROWS BETWEEN UNBOUNDED PRECEDING AND UNBOUNDED FOLLOWING
)

```

---

# 🔹 **Value & Distribution Functions**

```sql
CUME_DIST() OVER (
    [PARTITION BY column]
    ORDER BY column
)   -- cumulative distribution (0 < value ≤ 1)

PERCENT_RANK() OVER (
    [PARTITION BY column]
    ORDER BY column
)   -- relative rank between 0 and 1

PERCENTILE_CONT(fraction) WITHIN GROUP (ORDER BY column)
    OVER (PARTITION BY column)

PERCENTILE_DISC(fraction) WITHIN GROUP (ORDER BY column)
    OVER (PARTITION BY column)

```

# _What are Advanced Window Functions:_

_Advanced window functions are analytical SQL functions that perform complex calculations across a defined set of rows (window frame) related to the current row. They include positional functions (FIRST_VALUE, LAST_VALUE, NTH_VALUE), distribution functions (NTILE, CUME_DIST, PERCENT_RANK), and frame specifications that control exactly which rows to include in calculations._

- _FIRST_VALUE, LAST_VALUE, NTH_VALUE access specific positioned values within a window._
- _NTILE divides data into equal groups (quartiles, percentiles, etc.)._
- _CUME_DIST and PERCENT_RANK provide statistical distribution information._
- _Frame Clause precisely controls which rows are included in the window._
- _Window Clause allows reusing window definitions for cleaner code._

## _**Why Use Advanced Window Functions?**_

_These functions are essential for:_

- _Statistical analysis and percentile calculations in business reporting._
- _Creating running totals, moving averages, and time-based calculations._
- _Accessing first/last values in groups without complex subqueries._
- _Distributing data into equal buckets for analysis (quartiles, deciles)._
- _Performance analytics, sales reporting, and data science applications._
- _Avoiding expensive self-joins and correlated subqueries._

---

# _🔹 FIRST_VALUE() Function_

_FIRST_VALUE() returns the first value in an ordered set within the window frame._

### _**Syntax:**_

```sql
FIRST_VALUE(column_name) OVER (
    [PARTITION BY column1, column2, ...]
    ORDER BY column1 [ASC|DESC], column2 [ASC|DESC], ...
    [frame_clause]
)

```

### _**Example 1: First Sale in Each Month**_

```sql
SELECT
    sales_date,
    salesperson,
    sale_amount,
    FIRST_VALUE(sale_amount) OVER (
        PARTITION BY EXTRACT(MONTH FROM sales_date)
        ORDER BY sales_date
        ROWS UNBOUNDED PRECEDING
    ) AS first_sale_of_month,
    FIRST_VALUE(salesperson) OVER (
        PARTITION BY EXTRACT(MONTH FROM sales_date)
        ORDER BY sales_date
        ROWS UNBOUNDED PRECEDING
    ) AS first_salesperson_of_month
FROM sales_data
ORDER BY sales_date;

```

_Result:_

```
sales_date | salesperson | sale_amount | first_sale_of_month | first_salesperson_of_month
-----------|-------------|-------------|--------------------|--------------------------
2024-01-05 | John        | 1000        | 1000               | John
2024-01-10 | Sarah       | 1500        | 1000               | John
2024-01-15 | Mike        | 800         | 1000               | John
2024-02-02 | Lisa        | 2000        | 2000               | Lisa
2024-02-08 | Tom         | 1200        | 2000               | Lisa

```

---

# _🔹 LAST_VALUE() Function_

_LAST_VALUE() returns the last value in an ordered set within the window frame._

### _**Syntax:**_

```sql
LAST_VALUE(column_name) OVER (
    [PARTITION BY column1, column2, ...]
    ORDER BY column1 [ASC|DESC], column2 [ASC|DESC], ...
    [frame_clause]
)

```

### _**⚠️ Important: Frame Clause Required**_

_Without proper frame clause, LAST_VALUE() only sees up to current row!_

### _**Example 2: Last Sale in Each Month**_

```sql
SELECT
    sales_date,
    salesperson,
    sale_amount,
    LAST_VALUE(sale_amount) OVER (
        PARTITION BY EXTRACT(MONTH FROM sales_date)
        ORDER BY sales_date
        ROWS BETWEEN UNBOUNDED PRECEDING AND UNBOUNDED FOLLOWING
    ) AS last_sale_of_month,
    LAST_VALUE(salesperson) OVER (
        PARTITION BY EXTRACT(MONTH FROM sales_date)
        ORDER BY sales_date
        ROWS BETWEEN UNBOUNDED PRECEDING AND UNBOUNDED FOLLOWING
    ) AS last_salesperson_of_month
FROM sales_data
ORDER BY sales_date;

```

---

# _🔹 Frame Clause - The Heart of Window Functions_

_Frame Clause defines exactly which rows within the partition are included in the window calculation._

### _**Complete Frame Syntax:**_

```sql
{ROWS | RANGE} BETWEEN frame_start AND frame_end

```

### _**Frame Boundaries:**_

- _UNBOUNDED PRECEDING - From the first row of partition_
- _UNBOUNDED FOLLOWING - To the last row of partition_
- _CURRENT ROW - The current row_
- _n PRECEDING - n rows before current row_
- _n FOLLOWING - n rows after current row_

### _**Common Frame Patterns:**_

### _1. Default Frame (Problematic for LAST_VALUE)_

```sql
-- ❌ Default frame: RANGE UNBOUNDED PRECEDING AND CURRENT ROW
LAST_VALUE(amount) OVER (ORDER BY date)  -- Only sees up to current row!

```

### _2. Full Partition Frame_

```sql
-- ✅ See entire partition
ROWS BETWEEN UNBOUNDED PRECEDING AND UNBOUNDED FOLLOWING

```

### _3. Moving Window Frame_

```sql
-- ✅ 3-row moving window (previous, current, next)
ROWS BETWEEN 1 PRECEDING AND 1 FOLLOWING

```

### _4. Running Total Frame_

```sql
-- ✅ Running total from start to current
ROWS UNBOUNDED PRECEDING

```

### _**Example 3: Frame Clause Comparison**_

```sql
SELECT
    sales_date,
    daily_sales,

    -- Moving 3-day average
    AVG(daily_sales) OVER (
        ORDER BY sales_date
        ROWS BETWEEN 1 PRECEDING AND 1 FOLLOWING
    ) AS moving_3day_avg,

    -- Running total
    SUM(daily_sales) OVER (
        ORDER BY sales_date
        ROWS UNBOUNDED PRECEDING
    ) AS running_total,

    -- Last value with correct frame
    LAST_VALUE(daily_sales) OVER (
        ORDER BY sales_date
        ROWS BETWEEN UNBOUNDED PRECEDING AND UNBOUNDED FOLLOWING
    ) AS max_sales_in_dataset

FROM daily_sales
ORDER BY sales_date;

```

---

# _🔹 Window Clause - Reusing Window Definitions_

_Window Clause allows you to define a window once and reuse it multiple times for cleaner code._

### _**Syntax:**_

```sql
SELECT columns...
FROM table
WINDOW window_name AS (
    [PARTITION BY column1, column2, ...]
    [ORDER BY column1 [ASC|DESC], column2 [ASC|DESC], ...]
    [frame_clause]
)

```

### _**Example 4: Using Window Clause**_

```sql
-- ❌ Without Window Clause (Repetitive)
SELECT
    employee_id,
    salary,
    FIRST_VALUE(salary) OVER (PARTITION BY department ORDER BY salary DESC) AS highest_in_dept,
    LAST_VALUE(salary) OVER (PARTITION BY department ORDER BY salary DESC ROWS BETWEEN UNBOUNDED PRECEDING AND UNBOUNDED FOLLOWING) AS lowest_in_dept,
    AVG(salary) OVER (PARTITION BY department ORDER BY salary DESC ROWS BETWEEN UNBOUNDED PRECEDING AND UNBOUNDED FOLLOWING) AS avg_dept_salary
FROM employees;

-- ✅ With Window Clause (Clean)
SELECT
    employee_id,
    salary,
    FIRST_VALUE(salary) OVER w AS highest_in_dept,
    LAST_VALUE(salary) OVER w AS lowest_in_dept,
    AVG(salary) OVER w AS avg_dept_salary
FROM employees
WINDOW w AS (
    PARTITION BY department
    ORDER BY salary DESC
    ROWS BETWEEN UNBOUNDED PRECEDING AND UNBOUNDED FOLLOWING
);

```

---

# _🔹 NTH_VALUE() Function_

_NTH_VALUE() returns the value at a specific position (nth row) within the window frame._

### _**Syntax:**_

```sql
NTH_VALUE(column_name, n) OVER (
    [PARTITION BY column1, column2, ...]
    ORDER BY column1 [ASC|DESC], column2 [ASC|DESC], ...
    [frame_clause]
)

```

### _**Example 5: Getting 2nd and 3rd Highest Salaries**_

```sql
SELECT
    employee_id,
    first_name,
    department,
    salary,
    NTH_VALUE(salary, 1) OVER w AS highest_salary,
    NTH_VALUE(salary, 2) OVER w AS second_highest,
    NTH_VALUE(salary, 3) OVER w AS third_highest,
    NTH_VALUE(first_name, 2) OVER w AS second_highest_employee
FROM employees
WINDOW w AS (
    PARTITION BY department
    ORDER BY salary DESC
    ROWS UNBOUNDED PRECEDING
)
ORDER BY department, salary DESC;

```

_Result:_

```
employee_id | first_name | department | salary | highest_salary | second_highest | third_highest | second_highest_employee
------------|------------|------------|--------|----------------|----------------|---------------|------------------------
101         | John       | IT         | 75000  | 75000          | NULL           | NULL          | NULL
102         | Sarah      | IT         | 70000  | 75000          | 70000          | NULL          | Sarah
103         | Mike       | IT         | 65000  | 75000          | 70000          | 65000         | Sarah

```

---

# _🔹 NTILE() Function_

_NTILE() divides the result set into n roughly equal groups and assigns a group number to each row._

### _**Syntax:**_

```sql
NTILE(number_of_groups) OVER (
    [PARTITION BY column1, column2, ...]
    ORDER BY column1 [ASC|DESC], column2 [ASC|DESC], ...
)

```

### _**Example 6: Quartile Analysis**_

```sql
SELECT
    employee_id,
    first_name,
    salary,
    NTILE(4) OVER (ORDER BY salary DESC) AS salary_quartile,
    NTILE(10) OVER (ORDER BY salary DESC) AS salary_decile,
    NTILE(100) OVER (ORDER BY salary DESC) AS salary_percentile,

    -- Quartile within department
    NTILE(4) OVER (
        PARTITION BY department
        ORDER BY salary DESC
    ) AS dept_quartile
FROM employees
ORDER BY salary DESC;

```

_Result:_

```
employee_id | first_name | salary | salary_quartile | salary_decile | salary_percentile | dept_quartile
------------|------------|--------|-----------------|---------------|-------------------|---------------
101         | John       | 95000  | 1               | 1             | 1                 | 1
102         | Sarah      | 90000  | 1               | 1             | 2                 | 1
103         | Mike       | 85000  | 1               | 2             | 3                 | 2
104         | Lisa       | 80000  | 2               | 2             | 4                 | 2

```

### _**NTILE Use Cases:**_

- _Customer segmentation (high, medium, low value)_
- _Performance ranking (top 10%, middle 80%, bottom 10%)_
- _A/B testing group assignments_
- _Sales territory balancing_

---

# _🔹 CUME_DIST() Function_

_CUME_DIST() calculates the cumulative distribution (percentile) of a value within a group. Returns values between 0 and 1._

### _**Syntax:**_

```sql
CUME_DIST() OVER (
    [PARTITION BY column1, column2, ...]
    ORDER BY column1 [ASC|DESC], column2 [ASC|DESC], ...
)

```

### _**Formula:**_

_CUME_DIST = (Number of rows with values <= current row value) / (Total number of rows)_

### _**Example 7: Cumulative Distribution Analysis**_

```sql
SELECT
    student_id,
    student_name,
    exam_score,
    CUME_DIST() OVER (ORDER BY exam_score) AS overall_percentile,
    ROUND(CUME_DIST() OVER (ORDER BY exam_score) * 100, 2) AS percentile_score,

    -- Within class percentile
    CUME_DIST() OVER (
        PARTITION BY class_id
        ORDER BY exam_score
    ) AS class_percentile,

    -- Interpretation
    CASE
        WHEN CUME_DIST() OVER (ORDER BY exam_score) >= 0.9 THEN 'Top 10%'
        WHEN CUME_DIST() OVER (ORDER BY exam_score) >= 0.75 THEN 'Top 25%'
        WHEN CUME_DIST() OVER (ORDER BY exam_score) >= 0.5 THEN 'Above Average'
        ELSE 'Below Average'
    END AS performance_category
FROM student_scores
ORDER BY exam_score DESC;

```

_Result:_

```
student_id | student_name | exam_score | overall_percentile | percentile_score | class_percentile | performance_category
-----------|--------------|------------|-------------------|------------------|------------------|---------------------
101        | Alice        | 95         | 1.00              | 100.00           | 1.00             | Top 10%
102        | Bob          | 90         | 0.90              | 90.00            | 0.83             | Top 10%
103        | Charlie      | 85         | 0.80              | 80.00            | 0.67             | Top 25%
104        | David        | 75         | 0.60              | 60.00            | 0.50             | Above Average
105        | Eva          | 70         | 0.40              | 40.00            | 0.33             | Below Average

```

---

# _🔹 PERCENT_RANK() Function_

_PERCENT_RANK() calculates the relative rank of a row within a group as a percentage (0 to 1)._

### _**Syntax:**_

```sql
PERCENT_RANK() OVER (
    [PARTITION BY column1, column2, ...]
    ORDER BY column1 [ASC|DESC], column2 [ASC|DESC], ...
)

```

### _**Formula:**_

_PERCENT_RANK = (RANK - 1) / (Total rows - 1)_

### _**Example 8: Percent Rank vs CUME_DIST Comparison**_

```sql
SELECT
    employee_id,
    first_name,
    salary,
    RANK() OVER (ORDER BY salary DESC) AS salary_rank,
    PERCENT_RANK() OVER (ORDER BY salary DESC) AS percent_rank,
    ROUND(PERCENT_RANK() OVER (ORDER BY salary DESC) * 100, 2) AS percent_rank_pct,
    CUME_DIST() OVER (ORDER BY salary DESC) AS cumulative_dist,
    ROUND(CUME_DIST() OVER (ORDER BY salary DESC) * 100, 2) AS cume_dist_pct,

    -- Difference explanation
    ROUND((CUME_DIST() OVER (ORDER BY salary DESC) -
           PERCENT_RANK() OVER (ORDER BY salary DESC)) * 100, 2) AS difference_pct
FROM employees
ORDER BY salary DESC;

```

_Result:_

```
employee_id | first_name | salary | salary_rank | percent_rank | percent_rank_pct | cumulative_dist | cume_dist_pct | difference_pct
------------|------------|--------|-------------|--------------|------------------|-----------------|---------------|----------------
101         | John       | 95000  | 1           | 0.00         | 0.00             | 0.20            | 20.00         | 20.00
102         | Sarah      | 90000  | 2           | 0.25         | 25.00            | 0.40            | 40.00         | 15.00
103         | Mike       | 85000  | 3           | 0.50         | 50.00            | 0.60            | 60.00         | 10.00
104         | Lisa       | 80000  | 4           | 0.75         | 75.00            | 0.80            | 80.00         | 5.00
105         | Tom        | 75000  | 5           | 1.00         | 100.00           | 1.00            | 100.00        | 0.00

```

---

# _🔹 Complete Real-World Example_

### _**Example 9: Comprehensive Sales Analysis**_

```sql
WITH sales_analysis AS (
    SELECT
        salesperson_id,
        salesperson_name,
        region,
        monthly_sales,
        sales_month,

        -- Position functions
        FIRST_VALUE(monthly_sales) OVER w_region AS region_highest_sale,
        LAST_VALUE(monthly_sales) OVER w_region_full AS region_lowest_sale,
        NTH_VALUE(monthly_sales, 2) OVER w_region AS region_second_highest,

        -- Ranking and distribution
        NTILE(4) OVER w_company AS company_quartile,
        NTILE(3) OVER w_region AS region_tier,
        CUME_DIST() OVER w_company AS company_percentile,
        PERCENT_RANK() OVER w_region AS region_percent_rank,

        -- Moving calculations
        AVG(monthly_sales) OVER w_moving AS three_month_avg,
        SUM(monthly_sales) OVER w_running AS ytd_sales

    FROM sales_data

    WINDOW
        w_region AS (PARTITION BY region ORDER BY monthly_sales DESC),
        w_region_full AS (PARTITION BY region ORDER BY monthly_sales DESC
                         ROWS BETWEEN UNBOUNDED PRECEDING AND UNBOUNDED FOLLOWING),
        w_company AS (ORDER BY monthly_sales DESC),
        w_moving AS (PARTITION BY salesperson_id ORDER BY sales_month
                    ROWS BETWEEN 1 PRECEDING AND 1 FOLLOWING),
        w_running AS (PARTITION BY salesperson_id ORDER BY sales_month
                     ROWS UNBOUNDED PRECEDING)
)
SELECT
    salesperson_name,
    region,
    monthly_sales,
    region_highest_sale,
    region_second_highest,
    CASE company_quartile
        WHEN 1 THEN 'Top Performer'
        WHEN 2 THEN 'High Performer'
        WHEN 3 THEN 'Average Performer'
        WHEN 4 THEN 'Needs Improvement'
    END AS performance_category,
    ROUND(company_percentile * 100, 1) AS company_percentile_pct,
    three_month_avg,
    ytd_sales
FROM sales_analysis
ORDER BY monthly_sales DESC;

```

---

# _🔹 Quick Reference Syntax Templates_

### _**Position Functions:**_

```sql
-- Get first, last, and nth values
FIRST_VALUE(column) OVER (PARTITION BY group ORDER BY sort_col ROWS UNBOUNDED PRECEDING)
LAST_VALUE(column) OVER (PARTITION BY group ORDER BY sort_col ROWS BETWEEN UNBOUNDED PRECEDING AND UNBOUNDED FOLLOWING)
NTH_VALUE(column, n) OVER (PARTITION BY group ORDER BY sort_col ROWS UNBOUNDED PRECEDING)

```

### _**Distribution Functions:**_

```sql
-- Divide into groups and get percentiles
NTILE(n) OVER (PARTITION BY group ORDER BY sort_col)
CUME_DIST() OVER (PARTITION BY group ORDER BY sort_col)
PERCENT_RANK() OVER (PARTITION BY group ORDER BY sort_col)

```

### _**Frame Clause Templates:**_

```sql
-- Common frame patterns
ROWS UNBOUNDED PRECEDING                           -- From start to current
ROWS BETWEEN UNBOUNDED PRECEDING AND UNBOUNDED FOLLOWING  -- Entire partition
ROWS BETWEEN 1 PRECEDING AND 1 FOLLOWING          -- 3-row window
ROWS BETWEEN 2 PRECEDING AND CURRENT ROW          -- Last 3 rows including current

```

---

# _🔹 Advantages of Advanced Window Functions_

1. _**Statistical Analysis Power**_
    - _Easy percentile and distribution calculations._
    - _Built-in statistical functions eliminate complex math._
2. _**Performance Benefits**_
    - _Single pass through data instead of multiple queries._
    - _Optimized by database engines for analytical workloads._
3. _**Code Simplification**_
    - _Window clause reduces repetitive code._
    - _Eliminates complex correlated subqueries._
4. _**Precise Frame Control**_
    - _Exact control over which rows participate in calculations._
    - _Flexible moving windows and running totals._
5. _**Business Intelligence Ready**_
    - _Perfect for dashboards, reports, and analytics._
    - _Natural fit for KPI calculations and trending._

---

# _🔹 Disadvantages/Limitations_

1. _**Memory and Performance Impact**_
    - _Large result sets may require significant memory for sorting._
    - _Complex frame clauses can be resource-intensive._
2. _**Learning Complexity**_
    - _Frame clause syntax can be confusing initially._
    - _Multiple concepts to master (partitions, frames, ordering)._
3. _**Database Compatibility**_
    - _Not all databases support all advanced window functions._
    - _Frame clause syntax may vary between systems._
4. _**Debugging Difficulty**_
    - _Complex window specifications can be hard to debug._
    - _Result verification requires understanding of internal mechanics._

---

# _🔹 Common Pitfalls and Solutions_

### _**Pitfall 1: LAST_VALUE without proper frame**_

```sql
-- ❌ Wrong: Only sees current row
LAST_VALUE(amount) OVER (ORDER BY date)

-- ✅ Correct: Sees entire partition
LAST_VALUE(amount) OVER (ORDER BY date ROWS BETWEEN UNBOUNDED PRECEDING AND UNBOUNDED FOLLOWING)

```

### _**Pitfall 2: Misunderstanding CUME_DIST vs PERCENT_RANK**_

```sql
-- CUME_DIST: What percentage of values are <= current value
-- PERCENT_RANK: What percentage of values are < current value

-- For salary ranking (higher is better), use DESC order
CUME_DIST() OVER (ORDER BY salary DESC)      -- Higher salary = higher percentile
PERCENT_RANK() OVER (ORDER BY salary DESC)   -- Higher salary = higher percent rank

```

### _**Pitfall 3: NTILE with uneven groups**_

```sql
-- With 10 rows divided into 3 groups: sizes will be 4, 3, 3
-- First groups get the extra rows
SELECT value, NTILE(3) OVER (ORDER BY value) as tile
FROM (VALUES (1),(2),(3),(4),(5),(6),(7),(8),(9),(10)) t(value);

```

---

_**✅ Advantages → Statistical power, performance benefits, code simplification, precise control, BI-ready.**_

_**❌ Disadvantages → Memory impact, learning complexity, compatibility issues, debugging difficulty.**_

_👉 Golden Rules:_

_**"Always use proper frame clause with LAST_VALUE"**_

_**"Use Window clause to avoid repetitive code"**_

_**"CUME_DIST for 'what percentage are <= me', PERCENT_RANK for 'what percentage are < me'"**_

_**"NTILE divides into roughly equal groups, first groups get extra rows"**_



_👉 Golden Rules:_  
_**"Use RANK() when you need gaps for ties, DENSE_RANK() when you don't"**_ _**"Use LAG() to look backward, LEAD() to look forward in your data"**_ _**"Always consider indexing PARTITION BY and ORDER BY columns for performance"**_