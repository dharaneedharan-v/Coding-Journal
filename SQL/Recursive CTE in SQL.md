

# *What is Recursive CTE (Common Table Expression):*

*A Recursive CTE is a special type of CTE that references itself to process hierarchical or tree-structured data. It consists of two parts: an anchor member (base case) and a recursive member that references the CTE itself, allowing it to traverse parent-child relationships, organizational structures, and nested data.*

- *Processes hierarchical data like organizational charts, file systems, category trees.*
- *Self-referencing query that builds results iteratively.*
- *Consists of anchor query (starting point) + recursive query (iteration logic).*
- *Essential for traversing unknown-depth hierarchical structures.*
- *Eliminates need for complex loops or multiple self-joins.*

## ***Why Use Recursive CTE?***

*Recursive CTEs are powerful for scenarios involving:*

- *Organizational hierarchies (manager-employee relationships).*
- *Product category trees and nested classifications.*
- *File/folder directory structures and navigation paths.*
- *Social network connections and friend-of-friend relationships.*
- *Bill of Materials (BOM) and component breakdowns.*
- *Geographic hierarchies (country → state → city → district).*
- *Menu systems and nested navigation structures.*
- *Graph traversal and pathfinding problems.*

---

# *🔹 Recursive CTE Syntax Structure*

### ***Complete Syntax:***
```sql
WITH RECURSIVE cte_name (column_list) AS (
    -- ANCHOR MEMBER (Base Case)
    SELECT initial_columns
    FROM base_table
    WHERE base_condition
    
    UNION ALL
    
    -- RECURSIVE MEMBER (Iterative Case)
    SELECT recursive_columns
    FROM base_table
    INNER JOIN cte_name ON join_condition
    WHERE recursive_condition
)
-- MAIN QUERY
SELECT * FROM cte_name;
```

### ***Key Components:***
1. ***ANCHOR MEMBER*** - *Starting point (root nodes)*
2. ***UNION ALL*** - *Combines anchor and recursive results*
3. ***RECURSIVE MEMBER*** - *Self-referencing part*
4. ***JOIN CONDITION*** - *Defines parent-child relationship*
5. ***TERMINATION*** - *Automatic when no more rows found*

---

# *🔹 Basic Hierarchical Data Example*

### ***Sample Employee Table:***
```sql
CREATE TABLE employees (
    employee_id INT PRIMARY KEY,
    employee_name VARCHAR(100),
    manager_id INT,
    department VARCHAR(50),
    salary DECIMAL(10,2)
);

INSERT INTO employees VALUES
(1, 'CEO John', NULL, 'Executive', 200000),
(2, 'VP Sales Mary', 1, 'Sales', 150000),
(3, 'VP Tech Bob', 1, 'Technology', 160000),
(4, 'Sales Mgr Alice', 2, 'Sales', 100000),
(5, 'Dev Mgr Charlie', 3, 'Technology', 120000),
(6, 'Sales Rep David', 4, 'Sales', 60000),
(7, 'Sales Rep Eva', 4, 'Sales', 65000),
(8, 'Developer Frank', 5, 'Technology', 80000),
(9, 'Developer Grace', 5, 'Technology', 85000),
(10, 'Junior Dev Henry', 8, 'Technology', 50000);
```

### ***Example 1: Complete Organizational Hierarchy***
```sql
WITH RECURSIVE org_hierarchy AS (
    -- ANCHOR: Start with top-level employees (CEOs)
    SELECT 
        employee_id,
        employee_name,
        manager_id,
        department,
        salary,
        0 AS level,                           -- Root level
        CAST(employee_name AS VARCHAR(1000)) AS hierarchy_path,
        CAST(employee_id AS VARCHAR(1000)) AS id_path
    FROM employees
    WHERE manager_id IS NULL
    
    UNION ALL
    
    -- RECURSIVE: Get subordinates
    SELECT 
        e.employee_id,
        e.employee_name,
        e.manager_id,
        e.department,
        e.salary,
        oh.level + 1,                         -- Increment level
        CONCAT(oh.hierarchy_path, ' -> ', e.employee_name) AS hierarchy_path,
        CONCAT(oh.id_path, ',', e.employee_id) AS id_path
    FROM employees e
    INNER JOIN org_hierarchy oh ON e.manager_id = oh.employee_id
)
SELECT 
    employee_id,
    REPEAT('  ', level) + employee_name AS indented_name,  -- Visual hierarchy
    level,
    hierarchy_path,
    department,
    salary
FROM org_hierarchy
ORDER BY level, employee_id;
```

*Result:*
```
employee_id | indented_name        | level | hierarchy_path                           | department  | salary
------------|---------------------|-------|------------------------------------------|-------------|--------
1           | CEO John            | 0     | CEO John                                 | Executive   | 200000
2           |   VP Sales Mary     | 1     | CEO John -> VP Sales Mary                | Sales       | 150000
3           |   VP Tech Bob       | 1     | CEO John -> VP Tech Bob                  | Technology  | 160000
4           |     Sales Mgr Alice | 2     | CEO John -> VP Sales Mary -> Sales Mgr Alice | Sales   | 100000
5           |     Dev Mgr Charlie | 2     | CEO John -> VP Tech Bob -> Dev Mgr Charlie | Technology | 120000
6           |       Sales Rep David | 3   | CEO John -> VP Sales Mary -> Sales Mgr Alice -> Sales Rep David | Sales | 60000
```

---

# *🔹 Advanced Use Cases and Examples*

### ***Example 2: Calculate Hierarchical Totals (Team Salary Costs)***
```sql
WITH RECURSIVE team_hierarchy AS (
    -- Anchor: Start with manager
    SELECT 
        employee_id,
        employee_name,
        manager_id,
        salary,
        0 as level
    FROM employees
    WHERE employee_id = 2  -- VP Sales Mary's team
    
    UNION ALL
    
    -- Recursive: Get all subordinates
    SELECT 
        e.employee_id,
        e.employee_name,
        e.manager_id,
        e.salary,
        th.level + 1
    FROM employees e
    INNER JOIN team_hierarchy th ON e.manager_id = th.employee_id
),
team_totals AS (
    SELECT 
        employee_id,
        employee_name,
        salary,
        level,
        SUM(salary) OVER () AS total_team_cost,
        COUNT(*) OVER () AS team_size
    FROM team_hierarchy
)
SELECT 
    employee_name,
    salary,
    level,
    total_team_cost,
    team_size,
    ROUND(salary * 100.0 / total_team_cost, 2) AS salary_percentage
FROM team_totals
ORDER BY level, employee_id;
```

### ***Example 3: Find All Paths to Root (Bottom-Up Traversal)***
```sql
WITH RECURSIVE employee_paths AS (
    -- Anchor: Start with specific employee
    SELECT 
        employee_id,
        employee_name,
        manager_id,
        0 AS levels_to_top,
        employee_name AS path_to_top
    FROM employees
    WHERE employee_id = 10  -- Henry (Junior Developer)
    
    UNION ALL
    
    -- Recursive: Go up the hierarchy
    SELECT 
        e.employee_id,
        e.employee_name,
        e.manager_id,
        ep.levels_to_top + 1,
        CONCAT(e.employee_name, ' -> ', ep.path_to_top) AS path_to_top
    FROM employees e
    INNER JOIN employee_paths ep ON e.employee_id = ep.manager_id
)
SELECT 
    employee_name,
    levels_to_top,
    path_to_top
FROM employee_paths
ORDER BY levels_to_top DESC;
```

### ***Example 4: Category Tree Navigation***
```sql
-- Product Categories Table
CREATE TABLE categories (
    category_id INT PRIMARY KEY,
    category_name VARCHAR(100),
    parent_category_id INT
);

INSERT INTO categories VALUES
(1, 'Electronics', NULL),
(2, 'Computers', 1),
(3, 'Mobile Phones', 1),
(4, 'Laptops', 2),
(5, 'Desktops', 2),
(6, 'Gaming Laptops', 4),
(7, 'Business Laptops', 4),
(8, 'Smartphones', 3),
(9, 'Feature Phones', 3);

-- Get all subcategories of Electronics
WITH RECURSIVE category_tree AS (
    -- Anchor: Start with main category
    SELECT 
        category_id,
        category_name,
        parent_category_id,
        0 AS depth,
        category_name AS full_path
    FROM categories
    WHERE category_name = 'Electronics'
    
    UNION ALL
    
    -- Recursive: Get subcategories
    SELECT 
        c.category_id,
        c.category_name,
        c.parent_category_id,
        ct.depth + 1,
        CONCAT(ct.full_path, ' / ', c.category_name)
    FROM categories c
    INNER JOIN category_tree ct ON c.parent_category_id = ct.category_id
)
SELECT 
    category_id,
    REPEAT('  ', depth) + category_name AS indented_category,
    depth,
    full_path
FROM category_tree
ORDER BY category_id;
```

---

# *🔹 Important Recursive CTE Interview Questions*

### ***Question 1: Find Number of Levels in Hierarchy***
```sql
WITH RECURSIVE hierarchy_depth AS (
    SELECT employee_id, employee_name, manager_id, 0 AS level
    FROM employees WHERE manager_id IS NULL
    
    UNION ALL
    
    SELECT e.employee_id, e.employee_name, e.manager_id, hd.level + 1
    FROM employees e
    JOIN hierarchy_depth hd ON e.manager_id = hd.employee_id
)
SELECT MAX(level) + 1 AS total_hierarchy_levels
FROM hierarchy_depth;
```

### ***Question 2: Find All Leaf Nodes (Employees with No Subordinates)***
```sql
WITH RECURSIVE all_employees AS (
    SELECT employee_id, employee_name, manager_id, 0 AS level
    FROM employees WHERE manager_id IS NULL
    
    UNION ALL
    
    SELECT e.employee_id, e.employee_name, e.manager_id, ae.level + 1
    FROM employees e
    JOIN all_employees ae ON e.manager_id = ae.employee_id
)
SELECT ae.employee_id, ae.employee_name, ae.level
FROM all_employees ae
LEFT JOIN employees subordinates ON ae.employee_id = subordinates.manager_id
WHERE subordinates.manager_id IS NULL  -- No subordinates = leaf node
ORDER BY ae.level DESC;
```

### ***Question 3: Find Common Manager of Two Employees***
```sql
WITH RECURSIVE emp1_hierarchy AS (
    -- Get hierarchy for employee 1
    SELECT employee_id, manager_id, 0 AS level
    FROM employees WHERE employee_id = 6  -- David
    
    UNION ALL
    
    SELECT e.employee_id, e.manager_id, eh.level + 1
    FROM employees e
    JOIN emp1_hierarchy eh ON e.employee_id = eh.manager_id
),
emp2_hierarchy AS (
    -- Get hierarchy for employee 2
    SELECT employee_id, manager_id, 0 AS level
    FROM employees WHERE employee_id = 8  -- Frank
    
    UNION ALL
    
    SELECT e.employee_id, e.manager_id, eh.level + 1
    FROM employees e
    JOIN emp2_hierarchy eh ON e.employee_id = eh.manager_id
)
SELECT e.employee_name AS common_manager
FROM employees e
WHERE e.employee_id IN (
    SELECT eh1.employee_id FROM emp1_hierarchy eh1
    INTERSECT
    SELECT eh2.employee_id FROM emp2_hierarchy eh2
)
ORDER BY (SELECT level FROM emp1_hierarchy WHERE employee_id = e.employee_id) ASC
LIMIT 1;
```

### ***Question 4: Calculate Span of Control (Direct Reports Count)***
```sql
WITH RECURSIVE org_structure AS (
    SELECT employee_id, employee_name, manager_id, 0 AS level
    FROM employees WHERE manager_id IS NULL
    
    UNION ALL
    
    SELECT e.employee_id, e.employee_name, e.manager_id, os.level + 1
    FROM employees e
    JOIN org_structure os ON e.manager_id = os.employee_id
)
SELECT 
    m.employee_name AS manager_name,
    COUNT(s.employee_id) AS direct_reports,
    CASE 
        WHEN COUNT(s.employee_id) = 0 THEN 'Individual Contributor'
        WHEN COUNT(s.employee_id) <= 3 THEN 'Small Team Lead'
        WHEN COUNT(s.employee_id) <= 7 THEN 'Medium Team Manager'
        ELSE 'Large Team Manager'
    END AS management_level
FROM employees m
LEFT JOIN employees s ON m.employee_id = s.manager_id
GROUP BY m.employee_id, m.employee_name
ORDER BY direct_reports DESC;
```

---

# *🔹 Complex Real-World Scenarios*

### ***Example 5: Bill of Materials (BOM) Explosion***
```sql
CREATE TABLE bom (
    component_id INT,
    component_name VARCHAR(100),
    parent_component_id INT,
    quantity_required INT,
    unit_cost DECIMAL(10,2)
);

INSERT INTO bom VALUES
(1, 'Bicycle', NULL, 1, 500.00),
(2, 'Frame', 1, 1, 200.00),
(3, 'Wheels', 1, 2, 50.00),
(4, 'Seat', 1, 1, 30.00),
(5, 'Handlebar', 1, 1, 25.00),
(6, 'Rim', 3, 1, 20.00),
(7, 'Tire', 3, 1, 15.00),
(8, 'Spokes', 3, 24, 0.50);

WITH RECURSIVE bom_explosion AS (
    -- Anchor: Top-level product
    SELECT 
        component_id,
        component_name,
        parent_component_id,
        quantity_required,
        unit_cost,
        0 AS level,
        CAST(quantity_required AS DECIMAL(10,2)) AS total_quantity,
        quantity_required * unit_cost AS extended_cost
    FROM bom
    WHERE parent_component_id IS NULL
    
    UNION ALL
    
    -- Recursive: Sub-components
    SELECT 
        b.component_id,
        b.component_name,
        b.parent_component_id,
        b.quantity_required,
        b.unit_cost,
        be.level + 1,
        be.total_quantity * b.quantity_required AS total_quantity,
        (be.total_quantity * b.quantity_required) * b.unit_cost AS extended_cost
    FROM bom b
    INNER JOIN bom_explosion be ON b.parent_component_id = be.component_id
)
SELECT 
    REPEAT('  ', level) + component_name AS indented_component,
    level,
    quantity_required,
    total_quantity,
    unit_cost,
    extended_cost,
    SUM(extended_cost) OVER() AS total_bom_cost
FROM bom_explosion
ORDER BY component_id;
```

### ***Example 6: Social Network Friend Connections***
```sql
CREATE TABLE friendships (
    user_id INT,
    friend_id INT
);

-- Find friends within 3 degrees of separation
WITH RECURSIVE friend_network AS (
    -- Anchor: Direct friends
    SELECT 
        user_id,
        friend_id,
        1 AS degree,
        CAST(user_id AS VARCHAR(1000)) + '->' + CAST(friend_id AS VARCHAR(1000)) AS path
    FROM friendships
    WHERE user_id = 1  -- Starting user
    
    UNION ALL
    
    -- Recursive: Friends of friends
    SELECT 
        fn.user_id,
        f.friend_id,
        fn.degree + 1,
        fn.path + '->' + CAST(f.friend_id AS VARCHAR(1000))
    FROM friend_network fn
    INNER JOIN friendships f ON fn.friend_id = f.user_id
    WHERE fn.degree < 3  -- Limit to 3 degrees
      AND f.friend_id != fn.user_id  -- Avoid circular references
      AND fn.path NOT LIKE '%' + CAST(f.friend_id AS VARCHAR(10)) + '%'  -- Avoid revisiting
)
SELECT DISTINCT
    friend_id,
    MIN(degree) AS closest_degree,
    COUNT(*) AS connection_paths
FROM friend_network
GROUP BY friend_id
ORDER BY closest_degree, friend_id;
```

---

# *🔹 Performance Optimization and Best Practices*

### ***Optimization Tips:***

#### *1. Add Termination Conditions*
```sql
WITH RECURSIVE hierarchy AS (
    SELECT employee_id, manager_id, 0 AS level
    FROM employees WHERE manager_id IS NULL
    
    UNION ALL
    
    SELECT e.employee_id, e.manager_id, h.level + 1
    FROM employees e
    JOIN hierarchy h ON e.manager_id = h.employee_id
    WHERE h.level < 10  -- Prevent infinite recursion
)
SELECT * FROM hierarchy;
```

#### *2. Use Proper Indexing*
```sql
-- Essential indexes for hierarchical queries
CREATE INDEX idx_employees_manager_id ON employees(manager_id);
CREATE INDEX idx_employees_employee_id ON employees(employee_id);
```

#### *3. Control Recursion Depth*
```sql
-- Database-specific recursion limits
-- SQL Server: OPTION (MAXRECURSION 100)
-- PostgreSQL: Uses default limit, can be adjusted
-- Oracle: Uses CONNECT BY instead of recursive CTE
```

---

# *🔹 Alternative Approaches to Recursive CTE*

### ***1. Nested Set Model***
```sql
-- Alternative: Store left/right boundaries
CREATE TABLE employees_nested (
    employee_id INT,
    employee_name VARCHAR(100),
    left_bound INT,
    right_bound INT
);

-- Find all subordinates with simple range query
SELECT * FROM employees_nested
WHERE left_bound > 2 AND right_bound < 15;  -- Much faster for large hierarchies
```

### ***2. Path Enumeration***
```sql
-- Store full path in materialized column
CREATE TABLE employees_path (
    employee_id INT,
    employee_name VARCHAR(100),
    manager_path VARCHAR(1000)  -- e.g., '1/2/4/' for employee under 1->2->4
);

-- Find subordinates with LIKE query
SELECT * FROM employees_path
WHERE manager_path LIKE '1/2/%';
```

### ***3. Closure Table***
```sql
-- Store all ancestor-descendant relationships
CREATE TABLE employee_closure (
    ancestor_id INT,
    descendant_id INT,
    depth INT
);

-- Direct query for hierarchical relationships
SELECT * FROM employee_closure WHERE ancestor_id = 2;  -- All subordinates of employee 2
```

---

# *🔹 Advantages of Recursive CTE*

1. ***Natural Hierarchical Processing***
   - *Intuitive for tree-structured data.*
   - *Handles unknown-depth hierarchies automatically.*

2. ***Single Query Solution***
   - *Eliminates need for application-level loops.*
   - *Reduces round trips between application and database.*

3. ***Standard SQL Compliance***
   - *Portable across different database systems.*
   - *Part of SQL standard (SQL:1999 and later).*

4. ***Dynamic Depth Handling***
   - *Works with hierarchies of any depth.*
   - *No need to know maximum levels in advance.*

5. ***Flexible Path Building***
   - *Can build paths, calculate levels, aggregate values.*
   - *Easy to add business logic during traversal.*

---

# *🔹 Disadvantages and Limitations*

1. ***Performance Issues***
   - *Can be slow on large hierarchies without proper indexing.*
   - *Memory-intensive for deep or wide hierarchies.*

2. ***Risk of Infinite Recursion***
   - *Circular references can cause infinite loops.*
   - *Requires careful termination conditions.*

3. ***Database-Specific Limitations***
   - *Maximum recursion depth varies by database.*
   - *Some databases don't support recursive CTEs.*

4. ***Complex Debugging***
   - *Difficult to debug recursive logic.*
   - *Hard to trace execution flow.*

5. ***Limited Parallel Processing***
   - *Recursive nature makes parallelization difficult.*
   - *Sequential processing can be bottleneck.*

---

# *🔹 Common Pitfalls and Solutions*

### ***Pitfall 1: Infinite Recursion***
```sql
-- ❌ Dangerous: No termination condition
WITH RECURSIVE bad_cte AS (
    SELECT 1 AS n
    UNION ALL
    SELECT n + 1 FROM bad_cte  -- Will run forever!
)
SELECT * FROM bad_cte;

-- ✅ Safe: Add termination condition
WITH RECURSIVE safe_cte AS (
    SELECT 1 AS n
    UNION ALL
    SELECT n + 1 FROM safe_cte WHERE n < 100
)
SELECT * FROM safe_cte;
```

### ***Pitfall 2: Circular References***
```sql
-- ✅ Detect and prevent circular references
WITH RECURSIVE hierarchy_safe AS (
    SELECT employee_id, manager_id, 
           CAST(employee_id AS VARCHAR(1000)) AS path
    FROM employees WHERE manager_id IS NULL
    
    UNION ALL
    
    SELECT e.employee_id, e.manager_id,
           hs.path + ',' + CAST(e.employee_id AS VARCHAR(10))
    FROM employees e
    JOIN hierarchy_safe hs ON e.manager_id = hs.employee_id
    WHERE hs.path NOT LIKE '%,' + CAST(e.employee_id AS VARCHAR(10)) + ',%'  -- Prevent cycles
)
SELECT * FROM hierarchy_safe;
```

### ***Pitfall 3: Missing Base Case***
```sql
-- ❌ Wrong: No anchor member
WITH RECURSIVE broken_cte AS (
    SELECT e.employee_id FROM employees e
    JOIN broken_cte bc ON e.manager_id = bc.employee_id  -- Missing base case
)
SELECT * FROM broken_cte;

-- ✅ Correct: Always have anchor member
WITH RECURSIVE working_cte AS (
    SELECT employee_id FROM employees WHERE manager_id IS NULL  -- Anchor
    UNION ALL
    SELECT e.employee_id FROM employees e
    JOIN working_cte wc ON e.manager_id = wc.employee_id  -- Recursive
)
SELECT * FROM working_cte;
```

---

# *🔹 Database-Specific Considerations*

### ***SQL Server***
```sql
-- SQL Server syntax and limitations
WITH hierarchy AS (
    -- anchor and recursive members
)
SELECT * FROM hierarchy
OPTION (MAXRECURSION 1000);  -- Control max recursion
```

### ***PostgreSQL***
```sql
-- PostgreSQL supports standard recursive CTE
WITH RECURSIVE hierarchy AS (
    -- anchor and recursive members
)
SELECT * FROM hierarchy;
```

### ***Oracle (Alternative Approach)***
```sql
-- Oracle uses CONNECT BY instead
SELECT employee_id, manager_id, LEVEL
FROM employees
START WITH manager_id IS NULL
CONNECT BY PRIOR employee_id = manager_id;
```

### ***MySQL***
```sql
-- MySQL 8.0+ supports recursive CTE
WITH RECURSIVE hierarchy AS (
    -- anchor and recursive members
)
SELECT * FROM hierarchy;
```

---

***✅ Advantages → Natural hierarchical processing, single query solution, SQL standard, dynamic depth, flexible path building.***  
***❌ Disadvantages → Performance issues, infinite recursion risk, database limitations, debugging complexity, limited parallelization.***

*👉 Golden Rules:*  
***"Always include proper termination conditions to prevent infinite recursion"***  
***"Index manager_id and employee_id columns for better performance"***  
***"Check for circular references in your data before using recursive CTEs"***  
***"Consider alternative approaches (nested set, closure table) for very large hierarchies"***  
***"Use UNION ALL (not UNION) in recursive CTEs for better performance"***