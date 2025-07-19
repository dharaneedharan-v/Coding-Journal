
TEMPLATE FOR THE LCS : 

For the both Print and Max length 

```python 
class Solution
		def LCS(N , M ):
		    if (N)  == len(s1) or (M) == len(s2):
		        return ""
		    if s1[N] == s2[M]:
		      #  return 1 + LCS(N+1 , M+1  )
		      return s1[N] + LCS(N+1,M+1)
		    else :
		      #  return max(LCS(N+1 , M) , LCS(N, M+1 ))
		      First = LCS(N+1 , M)
		      Second = LCS(N , M+1)
		      return First if len(First)>len(Second) else Second
		        
		dk = LCS(0 , 0)
		print(dk )
		return ""
```

To print The longest Substring Using the DP : 

```python 
class Solution:
    def longestCommonSubsequence(self, text1: str, text2: str) -> int:
        N = len(text1)
        M = len(text2)
        dp = [ [ "" for _ in range(M+1)] for _ in range((N+1))]
        # print(dp)
        for i in range(N-1 , -1 , -1):
            for j in range(M-1 , -1 , -1):
                if text1[i] == text2[j] :
                    dp[i][j] = text1[i]+dp[i+1][j+1]
                else :
                    if len(dp[i+1][j]) > len(dp[i][j+1]):
                        dp[i][j] = dp[i+1][j]
                    else :
                        dp[i][j] = dp[i][j+1]
        print(dp[0][0])
        return dp[0][0]
```

===============================================================
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



### DP ON STRING : 


### [1143. Longest Common Subsequence](https://leetcode.com/problems/longest-common-subsequence/) 

Using the Normal Recusion : ==> TLE 



LCS : 
```python 
class Solution:
    def longestCommonSubsequence(self, text1: str, text2: str) -> int:

        def REC ( N  ,  M , count  ):
            if N == len(text1) or M == len(text2):
                return count 
            if text1[N] == text2[M]:
                return REC(N+1  , M+1 , count+1 )
            else :
                return max( REC(N+1  , M , count ) , REC( N,M+1,count ) )


        return REC (0 , 0 , 0 )
```

Using the Memo :

```python 

class Solution:
    def longestCommonSubsequence(self, text1: str, text2: str) -> int:
        Mem = {}

        def REC ( N  ,  M   ):
            if N == len(text1) or M == len(text2):
                return 0

            if ( N  , M  ) in Mem :
                return Mem[(N , M)]

            if text1[N] == text2[M]:
                Mem[N , M] =  1+  REC(N+1  , M+1 )
                return Mem[N , M ]
            
            else :
                Mem[N , M ] = max(REC(N+1   , M ) , REC(N , M+1))
                return Mem[N , M ]
        return REC (0 , 0  )

```


### [516. Longest Palindromic Subsequence](https://leetcode.com/problems/longest-palindromic-subsequence/)


Using the Recursion ==> TLE :

```python 
class Solution:
    def longestPalindromeSubseq(self, s: str) -> int:
        S = s[::-1]
        # Memo = {}
        def Rec (N  , M ):
            if N ==len(s) or M == len(S):
                return 0 
            
            if s[N] == S[M]:
                return 1+ Rec(N+1  , M +1 )
            else :
                return max(Rec(N+1 , M ) , Rec(N , M+1))
        return Rec(0 , 0)
```


Using  The  Memo  : 

```python 
class Solution:
    def longestPalindromeSubseq(self, s: str) -> int:
        S = s[::-1]
        Memo = {}
        # @lru_cache(None)
        def Rec (N  , M ):
            if N == len(s) or M == len(S):
                return 0 
            if (N , M ) in Memo :
                return Memo[N , M]

            if s[N] == S[M]:
                Memo[N , M ] = 1+ Rec(N+1 , M +1)
                return Memo[N , M]
                # return 1+ Rec(N+1  , M +1 )
            else :
                Memo[N , M ] = max(Rec(N+1 , M ) , Rec(N , M+1))
                return Memo[N , M ]
                # return max(Rec(N+1 , M ) , Rec(N , M+1))
        return Rec(0 , 0)
```



### [1312. Minimum Insertion Steps to Make a String Palindrome](https://leetcode.com/problems/minimum-insertion-steps-to-make-a-string-palindrome/)

```python 
class Solution:
    def minInsertions(self, s: str) -> int:
        @lru_cache(None)
        def REC ( N  , M ):
            if N == len(s) or M == len(S):
                return 0 
            if s[N] == S[M]:
                return  1+ REC(N+1  , M+1 )
            else :
                return max( REC(N+1  , M   ) , REC( N,M+1 ) )

        def Longestpalindrom(s):
            S = s[::-1]
            return S
        S = Longestpalindrom(s)
        dk = REC(0,0)
        return len(s) - dk  

```

### [583. Delete Operation for Two Strings](https://leetcode.com/problems/delete-operation-for-two-strings/)

Using the LCS Template.. 

```python 
class Solution:
    def minDistance(self, word1: str, word2: str) -> int:
        @lru_cache(None)
        def LCS(N , M ):
            if  N == len(word1) or M == len(word2):
                return  0 
            if word1[N] == word2[M]:
                return 1 + LCS(N+1  , M +1 )
            else :
                return max(LCS(N+1 , M) , LCS(N , M+1))
        LongestSub = LCS(0 , 0 )
        deletion = len(word1) - LongestSub
        Insertion = len(word2) - LongestSub

        return deletion + Insertion

```



### Longest Common Substring

Using the LCS Tabulation Template.... 

To print and To get the Length also.. 

```python 
class Solution:
    def longestCommonSubstr(self, s1, s2):
        N = len(s1)
        M = len(s2)
        # dp = [ [ "" for _ in range(M+1)] for _ in range(N+1)] To print the String
        dp = [ [ 0 for _ in range(M+1)] for _ in range(N+1)]
        # print(dp)
        # Res = ""
        Max = 0 
        for i in range(N-1 , -1 , -1):
            for j in range(M-1 , -1 , -1):
                if s1[i] == s2[j]:
                    dp[i][j] = 1 + dp[i+1][j+1]
                    Max = max(Max , dp[i][j])
                    # if len(dp[i][j])> len(Res):
                    #     Res  = dp[i][j]
                else :
                    dp[i][j] = 0 
                    # dp[i][j] = ""
        # print(Res)
        # return len(Res)
        return Max 
                
```


