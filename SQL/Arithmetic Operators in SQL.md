

# 🔹 Salary Decrease Examples

### ✅ Decrease salary by 5%

```sql
UPDATE employees
SET salary = salary * 95 / 100;

```

👉 Take 95% of the salary (100% – 5% = 95%).

---

### ✅ Decrease salary by 10%

```sql
UPDATE employees
SET salary = salary * 90 / 100;

```

👉 Take 90% of the salary.

---

### ✅ Decrease salary by 25%

```sql
UPDATE employees
SET salary = salary * 75 / 100;

```

👉 Take 75% of the salary.

---

# 🔹 Salary Increase Examples

### ✅ Increase salary by 5%

```sql
UPDATE employees
SET salary = salary * 105 / 100;

```

👉 Take 100% of salary + 5% = 105%.

---

### ✅ Increase salary by 10%

```sql
UPDATE employees
SET salary = salary * 110 / 100;

```

👉 Take 100% of salary + 10% = 110%.

---

### ✅ Increase salary by 25%

```sql
UPDATE employees
SET salary = salary * 125 / 100;

```

👉 Take 100% of salary + 25% = 125%.

---

# 🔹 Example in Action

If salary = **10,000**:

- `salary * 95 / 100` → 9,500 (5% decrease)
- `salary * 90 / 100` → 9,000 (10% decrease)
- `salary * 105 / 100` → 10,500 (5% increase)
- `salary * 125 / 100` → 12,500 (25% increase)



Example  :


### Reduce salary by 5% for IT employees earning more than 60,000.

✅ Answer:

```sql
UPDATE employees
SET salary = salary * 0.95
WHERE department = 'IT' AND salary > 60000;

```


