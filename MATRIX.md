
Getting the input and Output from the User


```python 
rows = int(input())
cols = int(input())

matrix = [[0]*cols for _ in range(rows)]

for i in range(rows):
    for j in range(cols):
        matrix[i][j] = int(input())

print(matrix)
```

A Empty Matrix   Initialization : 


```python 
rows = 3
cols = 4

matrix = [[0 for _ in range(cols)] for _ in range(rows)]
print(matrix)

```

Gettting One By One : 


```python 
rows = int(input("Enter number of rows: "))
cols = int(input("Enter number of columns: "))

matrix = []

for i in range(rows):
    row = []
    for j in range(cols):
        val = int(input(f"Enter value for [{i}][{j}]: "))
        row.append(val)
    matrix.append(row)

print("Matrix:", matrix)
```