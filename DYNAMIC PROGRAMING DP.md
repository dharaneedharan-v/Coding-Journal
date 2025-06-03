
### [70. Climbing Stairs](https://leetcode.com/problems/climbing-stairs/)

```PYTHON 
class Solution:

    def climbStairs(self, n: int) -> int:

        if n == 1 :

            return 1

        dp = [-1]*(n+1)

        dp [1] = 1

        dp[2] = 2

        for i in range(3, n+1):

            dp[i] = dp[i-1]+dp[i-2]

        return dp[n]
```
### Frog Jump

```python 
class Solution:
    def minCost(self, height):
        dp = [0]* (len(height))
        dp[0]= 0 
        two = float('inf')
        for  i in range(1,len(height)):
            one = dp[i-1] + abs(height[i]-height[i-1])
            if i > 1 :
                two = dp[i-2] + abs(height[i]-height[i-2]) 
            dp[i]  = min(two, one)
        return dp[-1]
```

### Minimal Cost

```python 
class Solution:
    def minimizeCost(self, k, arr):
        # code here
        n = len(arr) 
        dp = [0]*n
        dp[0] = 0
        for i in range(1,n):
            Min = float('inf')
            for j in range(1, k+1):
                if i -j >= 0 :
                    one = dp[i-j]+ abs(arr[i] -arr[i-j])
                    Min = min(Min, one)
            dp [i] = Min 
        return dp[-1]
```


### [198. House Robber](https://leetcode.com/problems/house-robber/)


```python 
class Solution:

    def rob(self, nums: List[int]) -> int:

        if len(nums) == 1:

            return nums[0]

        if len(nums) == 2 :

            return max(nums[0], nums[1])

        n = len(nums)

        dp = [0] *(n)

        dp[0] = nums[0]

        dp[1] = max(nums[1], nums[0])

        for i in range(2,n):

            Max = dp[i-1] + nums[i-2]

            dp[i]   = max(dp[i-1], dp[i-2]+nums[i])

        print(dp)

        return dp[-1]
```


### [213. House Robber II](https://leetcode.com/problems/house-robber-ii/)


```python 
class Solution:

    def rob(self, nums: List[int]) -> int:

        def Max(nums):

            n = len(nums)

            if len(nums) == 1 :

                return nums[0]

            dp = [0] * n

            dp[0] = nums[0]

            dp[1] = max(nums[0],nums[1])

            for i in range(2, n):

                dp[i] = max (dp[i-1], nums[i]+dp[i-2])

            return dp[-1]

        if len(nums) == 1 :

            return nums[0]

        return max (Max(nums[:-1]), Max(nums[1:]))
```


# 2D DP : 

### [64. Minimum Path Sum](https://leetcode.com/problems/minimum-path-sum/)

```python 
class Solution:

    def minPathSum(self, grid: List[List[int]]) -> int:

        row = len(grid)

        col = len(grid[0])

        Matrix = [[0]*col for i in range(row)]

        # print(Matrix)

        Matrix[0][0] = grid[0][0]

        for i in range(1, row):

            Matrix[i][0] = Matrix[i-1][0]+grid[i][0]

        for i in range(1,col):

            Matrix[0][i] = Matrix[0][i-1] + grid[0][i]

        for  i in range(1, row):

            for j in range(1, col):

                Matrix[i][j] = min(Matrix[i-1][j], Matrix[i][j-1]) + grid[i][j]

        print(Matrix)

        return Matrix[-1][-1]
```


JUST TRY  : 

### [264. Ugly Number II](https://leetcode.com/problems/ugly-number-ii/)

Brute Force : Used Same logic in the Ugly number Finding.  

```python 
class Solution:
    def nthUglyNumber(self, n: int) -> int:
        if n <= 0 : return 0
        if n == 1 : return 1 
        def isugly(N : int ) -> bool :
            if N <= 0 :return False 
            while N % 2 ==  0:
                N = N // 2
            while N % 3 == 0 :
                N //= 3
            while N % 5 == 0 :
                N //= 5  
            return N == 1 
        count  = 0 
        dk = []
        for i in range(1, 1690*1000):
            if isugly(i) :
                dk.append(i)
                count += 1 
            if count == n :
                break 
        print(dk)
        return dk[count-1]
```

Optimized One : 

Remember the DP Pattern for this question 

```python 
class Solution:
    def nthUglyNumber(self, n: int) -> int:
        dp  = [1]
        i = j = k = 0 
        for  _ in range(n-1):
            Var = min(dp[i]* 2 , dp[j] * 3 , dp[k]* 5)
            dp.append(Var)
            if Var == dp[i]* 2 :
                i+= 1 
            if Var == dp[j]*  3 :
                j+= 1
            if Var == dp[k] * 5 :
                k += 1 
        return dp[-1]


```