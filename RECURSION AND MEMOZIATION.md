


TEMPLATE : 

Traversing : 

```python 

		def REC (N , M): 
            if M == len(N)  :
                return 
            else :
                print(N[M])
                REC(N , M+1)
        (REC(nums,0))
        
```
### Get a Strong Hold


### Sort a stack: 

```python 
class Solution:
    def Insert( self, S , N):
        if not S or S[-1] <= N : # S[-1] <= N is important..... 
            S.append(N)
        else :
            Temp = S.pop()
            self.Insert(S, N)
            S.append(Temp)
    def Sorted(self, s):
        if not s :
            return 
        else :
            temp = s.pop()
            self.Sorted(s)
            self.Insert(s , temp)
```


### Reverse a Stack

```python 

class Solution:
    def Insert(self , S , N):
        if not S :
            S.append(N)
        else :
            Temp = S.pop()
            self.Insert(S , N)
            S.append(Temp)
            
    def reverse(self,Stack):
        if not Stack :
            return 
        else :
            Temp = Stack.pop()
            self.reverse(Stack)
            self.Insert(Stack , Temp)
```



### [22. Generate Parentheses](https://leetcode.com/problems/generate-parentheses/) 



```python 
class Solution:
    def generateParenthesis(self, n: int) -> List[str]:
        def helper(Ans , Str , left , right ):
            if left == n and right == n :
                Ans.append(Str)
            if left <  n :
                helper(Ans , Str+"(" , left+1 , right)
            if right < n and right <  left  :
                helper(Ans , Str+")" , left , right + 1 ) 
        Ans = []
        Str = ""
        left = 0 
        right  = 0 
        helper(Ans , Str , left , right)
        return Ans 
```



### [17. Letter Combinations of a Phone Number](https://leetcode.com/problems/letter-combinations-of-a-phone-number/)


```python 

class Solution:
    def letterCombinations(self, digits: str) -> List[str]:
        Map = ["","","abc","def","ghi","jkl","mno","pqrs","tuv","wxyz"]
        Result = []
        def REC(idx  , lists):
            if idx == len(digits):
                Result.append(lists)
                return 
            dk = Map[int(digits[idx])]  # first take the Idx = 0 , 1 (2 , 3 ) the digit of the idx = "2" and Map it to the dictionary or list 
            # print(dk)
            for i in range(len(dk)):
                REC(idx+1 , lists + dk[i])
        Arr = ""
        REC(0 , Arr)
        return Result if len(digits) > 0 else []
```


### [39. Combination Sum](https://leetcode.com/problems/combination-sum/)


```python 
class Solution:
    def combinationSum(self, nums: List[int], Target: int) -> List[List[int]]:
        Result = []
        def REC(Nidx , Mlist , Sum):
            if Sum == Target:
                # Result.append(Mlist) Output :  [[],[],[]]
                Result.append(Mlist[:])
                return 
            if Sum > Target : # Another Base case for the Recusrion Tree to Stop it ...
                return 
            for i in range(Nidx , len(nums)):
                Mlist.append(nums[i]) #Include  ... 
                # REC(Nidx, Mlist , Sum+nums[i]) Output : [[2,2,3],[2,3,2],[3,2,2],[7]]
                REC(i, Mlist , Sum+nums[i])
                Mlist.pop() # Exclude or Remove or Dont pick it up... 
        Arr = []
        REC(0,Arr , 0 )
        return Result   
```
### [40. Combination Sum II](https://leetcode.com/problems/combination-sum-ii/)

```python 
class Solution:
    def combinationSum2(self, nums: List[int], Target: int) -> List[List[int]]:
        Result = []
        nums.sort()   # To eliminate the Duplicate.... 
        def REC(Nidx ,Mlist , Total):
            if Total == Target:
                dk = (Mlist[:])
                if dk not in Result :
                    Result.append(dk)
                return  
            if Total > Target :
                return 
            for i in range(Nidx  , len(nums)):
                if i > Nidx and nums[i] == nums[i-1]: # To eliminate the Same Element and Avoid the Duplicate of the elements
                    continue 
                Mlist.append(nums[i])
                REC(i+1  , Mlist , Total+nums[i])  # i+1 to avoid the current Element
                Mlist.pop()

        Arr = []
        REC(0,Arr,Total = 0 )
        return Result
```
### [216. Combination Sum III](https://leetcode.com/problems/combination-sum-iii/)

```python 
class Solution:
    def combinationSum3(self, k: int, n: int) -> List[List[int]]:
        Result = []
        def REC(Idx , Mlist , Total):
            if len(Mlist) == k and Total == n :
                Result.append(Mlist[:])
                return 
            if Total > n :
                return 
            for i in range(Idx , 10):
                Mlist.append(i)
                REC(i+1 , Mlist , Total+i)
                Mlist.pop()
        Arr = []
        REC(1, Arr , Total = 0 )
        return Result
        
```


### [78. Subsets](https://leetcode.com/problems/subsets/)

```python 
class Solution:
    def subsets(self, nums: List[int]) -> List[List[int]]:
        Result = []
        def REC(idx , Mlist ):
            if idx == len(nums):
                Result.append(Mlist)
                return 
            REC(idx+1 , Mlist)
            REC(idx+1 ,Mlist+ [nums[idx]])
        Arr = []
        REC(0 , Arr )
        return Result 
```


### [90. Subsets II](https://leetcode.com/problems/subsets-ii/)


```python 
class Solution:
    def subsetsWithDup(self, nums: List[int]) -> List[List[int]]:
        nums.sort()
        Result = []
        def REC(idx , Mlist):
            if idx == len(nums):
                dk = Mlist[:]
                if dk not in Result :
                    Result.append(dk)
                # Result.append(Mlist[:])
                return 
            REC(idx + 1 , Mlist)
            REC(idx +1 , Mlist+[nums[idx]])
        Arr = []
        REC(0, Arr)
        return Result 

```


```python 
class Solution:
    def subsetsWithDup(self, nums: List[int]) -> List[List[int]]:
        nums.sort()
        Result = []
        def REC(idx , Mlist):
            Result.append(Mlist[:]) 
            for i in range(idx , len(nums)):
                if i > idx and nums[i] == nums[i-1]:
                    continue 
                Mlist.append(nums[i])
                REC(i+1 , Mlist )
                Mlist .pop()
        Arr = []
        REC(0, Arr)
        return Result 

```


### [131. Palindrome Partitioning](https://leetcode.com/problems/palindrome-partitioning/)


```python 
class Solution:
    def partition(self, s: str) -> List[List[str]]:
        Result = []
        def Reversed(SubStr):
            if SubStr == SubStr[::-1]:
                return True 
            return False 

        def REC(idx , Mlist):
            if idx == len(s):
                Result.append(Mlist[:])
                return 
            for i in  range(idx , len(s)):
                Str = s[idx : i+1 ] ####
                if Reversed(Str): ####
                    Mlist.append(Str) ####
                    REC(i+1 , Mlist)
                    Mlist.pop()
            

        REC(0, [])
        return Result
```

-----
-----

### [62. Unique Paths](https://leetcode.com/problems/unique-paths/)


```python 
class Solution:
    def uniquePaths(self, m: int, n: int) -> int:
        i = j = 0 
        
        def DFS(i , j ):
            if i == m-1 and j == n -1:
                return 1 
            if i >= m or j >= n :return  0 
            return DFS(i+1 , j) + DFS(i , j+1 )
        return DFS(0 , 0 )
```

Memoziation : 

```python 
class Solution:
    def uniquePaths(self, m: int, n: int) -> int:
        i = j = 0 
        Memo = {}
        # @lru_cache
        def DFS(i , j ):
            if i == m-1 and j == n -1:
                return 1 
            if i >= m or j >= n :return  0 
            if (i , j ) in Memo :
                return Memo[(i , j)]
            Memo[(i , j )] = DFS(i+1  , j )+ DFS(i , j+1 )
            return Memo[(i,j)]
        return DFS(0 , 0 )
```


### [63. Unique Paths II](https://leetcode.com/problems/unique-paths-ii/)


If the Matrix Is given , Take the N = len(grid)  , M = len(grid[0]) Take it Simple Man... 

RECURSION : 
Get the TLE : 

```python 
class Solution:
    def uniquePathsWithObstacles(self, obstacleGrid: List[List[int]]) -> int:
        n = len(obstacleGrid)
        m = len(obstacleGrid[0])
        if obstacleGrid[0][0] == 1  or obstacleGrid[n-1][m-1] == 1 : return 0 
        def DFS (i , j ):
            if i == n-1 and j == m-1 : return 1 
            if i >= n or j >= m  or obstacleGrid[i][j] == 1 : return 0 
            down = DFS(i+1 , j )
            right = DFS(i, j+1)
            return down+ right 
        return DFS (0, 0)
```

MEMOZIATION:

Using the @LRU_CACHE : 
```python 
class Solution:
    def uniquePathsWithObstacles(self, obstacleGrid: List[List[int]]) -> int:
        n = len(obstacleGrid)
        m = len(obstacleGrid[0])
        if obstacleGrid[0][0] == 1  or obstacleGrid[n-1][m-1] == 1 : return 0 
        @lru_cache
        def DFS (i , j ):
            if i == n-1 and j == m-1 : return 1 
            if i >= n or j >= m  or obstacleGrid[i][j] == 1 : return 0 
            down = DFS(i+1 , j )
            right = DFS(i, j+1)
            return down+ right 
        return DFS (0, 0)
```

MEMOZIATION Using the Map  : 

```python 
class Solution:
    def uniquePathsWithObstacles(self, obstacleGrid: List[List[int]]) -> int:
        Memo = {}
        n = len(obstacleGrid)
        m = len(obstacleGrid[0])
        if obstacleGrid[0][0] == 1  or obstacleGrid[n-1][m-1] == 1 : return 0 
        def DFS (i , j ):
            if i == n-1 and j == m-1 : return 1 
            if i >= n or j >= m  or obstacleGrid[i][j] == 1 : return 0 
            if (i , j ) in Memo :
                return Memo[(i, j)]
            Memo[(i , j )] = DFS(i+1  , j )+ DFS(i , j+1 )
            return Memo[(i , j )]  
            # return Memo   TypeError: unsupported operand type(s) for +: 'int' and 'dict
        return DFS (0, 0)
```

