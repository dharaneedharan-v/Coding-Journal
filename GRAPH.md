### [695. Max Area of Island](https://leetcode.com/problems/max-area-of-island/)

```PYTHON 
class Solution:

    def maxAreaOfIsland(self, grid: List[List[int]]) -> int:

        row = len(grid)

        column = len(grid[0])

        count = 0

        for i in range(row):

            for j in range(column):

                if grid[i][j] == 0 :

                    continue

                count  = max(count,self.dfs(grid,i,j,row,column))

        return count

    def dfs(self, grid,i,j,row,column):

  

        if (i <0 or i >= row or j < 0 or j >=column or grid[i][j]==0):

            return 0

        grid[i][j] = 0

        count = 1

        count += self.dfs(grid, i+1,j,row,column)

        count += self.dfs(grid, i-1,j,row,column)

        count += self.dfs(grid, i,j+1,row,column)

        count += self.dfs(grid, i,j-1,row,column)

        return count
```

### [2658. Maximum Number of Fish in a Grid](https://leetcode.com/problems/maximum-number-of-fish-in-a-grid/)

```PYTHON 
class Solution:

    def findMaxFish(self, grid: List[List[int]]) -> int:

        row = len(grid)

        column = len(grid[0])

        Fish = 0

        for i in range(row):  # Iterate through rows

            for j in range(column):  # Iterate through columns

                if grid[i][j] == 0:

                    continue

                Fish = max(Fish, self.dfs(grid, i, j, row, column))  # Call dfs for each non-zero cell

        return Fish

  

    def dfs(self, grid, i, j, row, column):

        fish = 0

        if i < 0 or i >= row or j < 0 or j >= column or grid[i][j] == 0:

            return fish  # Base case, return 0 if out of bounds or no fish

        fish += grid[i][j]  # Add the current fish count

        grid[i][j] = 0  # Mark the cell as visited

        # Explore all 4 directions

        fish += self.dfs(grid, i, j+1, row, column)  # Right

        fish += self.dfs(grid, i+1, j, row, column)  # Down

        fish += self.dfs(grid, i, j-1, row, column)  # Left

        fish += self.dfs(grid, i-1, j, row, column)  # Up

        return fish
```