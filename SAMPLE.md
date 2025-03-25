
### [1. Two Sum](https://leetcode.com/problems/two-sum/)

```python 

class Solution:

    def twoSum(self, nums: List[int], target: int) -> List[int]:

        dd = {}

        for i in range(len(nums)):

            tar = target - nums[i]

            if tar in dd :

                return [dd[tar], i ]

            dd[nums[i]] = i

        return [-1,-1]
```


 O(N^2)

```python 
class Solution:

    def twoSum(self, nums: List[int], target: int) -> List[int]:

        for i in range(len(nums)):

            for j in range(i+1, len(nums)):

                if nums[i] + nums[j] == target :

                    return [i,j]
```


### [11. Container With Most Water](https://leetcode.com/problems/container-with-most-water/)

TLE : O(N^2)

```python 
class Solution:

    def maxArea(self, height: List[int]) -> int:

        Max  = 0

        for i in range(len(height)):

            for j in range(i,len(height)):

                width = abs(i - j)

                M_height = min(height[i],height[j])

                area = M_height * width

                Max = max(Max, area)

        return Max
```


O(N) 

```python 
class Solution:

    def maxArea(self, height: List[int]) -> int:

        n = len(height)

        l = 0

        r = n-1

        Max = 0

        while (l < r ):

            width = abs(r-l)

            Max_height  = min(height[l],height[r])

            area = width* Max_height

            Max = max(area, Max)

            if height[l] < height[r]:

                l = l+ 1

            elif(height[l] > height[r]) :

                r = r-1

                # An  edge case  to handle

            elif height[l] == height[r]:

                r = r-1

                l = l +1

            else :

                break

        return Max
```

### [15. 3Sum](https://leetcode.com/problems/3sum/)

TLE : 

O(N^2 ) :

```python 
class Solution:

    def threeSum(self, nums: List[int]) -> List[List[int]]:

        # dd = []

        dd = set()

        nums.sort() # To avoid the dupilcate of the pairs

        for i in range(len(nums)):

            for j in range(i+1 , len(nums)):

                for k in range(j+1 , len(nums)):

                    df = nums[i] +nums[j] + nums[k]

                    DS = (nums[i] ,nums[j] , nums[k]) # convert to tuple as the set will not allow to add it

                    if df == 0:

                        if DS not in dd:

                            dd.add(DS)

  

        return ([list(i) for  i in dd])
```

### [318. Maximum Product of Word Lengths](https://leetcode.com/problems/maximum-product-of-word-lengths/)


 TLE : 
O(N^2)

```python 
class Solution:

    def maxProduct(self, words: List[str]) -> int:

        Max = 0

        for i in range(len(words)):

            for j in range(i+1 , len(words)):

                if len(set(words[i]) & set(words[j])) == 0:

                    Max  = max(Max , len(words[i] * len(words[j])))

        return Max

```


```python 
class Solution:

    def maxProduct(self, words: List[str]) -> int:

        dd =[]

        for i in words:

            dd.append(set(i))

        print(dd)

        Max = 0

        for i in range(len(words)):

            for j in range(i+1 , len(words)):

                # Use the disjoint to check if the element has no common elements in build function

                if len(set(dd[i]) & set(dd[j])) == 0:

                    Max  = max(Max , len(words[i] * len(words[j])))

        return Max
```


### [76. Minimum Window Substring](https://leetcode.com/problems/minimum-window-substring/)


TLE : 
O(N^2)

```python 
class Solution:

    def minWindow(self, s: str, t: str) -> str:

        Min = float("inf")

        Min_str = ""

        def ischeck(sub, t) -> bool:

            return Counter(sub) >= Counter(t)    

        for i in range(len(s)):  

            for j in range(i + 1, len(s) + 1):

                substring = s[i:j]

                if ischeck(substring, t):

                    if len(substring) < Min:

                        Min = len(substring)

                        Min_str = substring

        return Min_str
```


### [844. Backspace String Compare](https://leetcode.com/problems/backspace-string-compare/)


```python 

class Solution:

    def backspaceCompare(self, s: str, t: str) -> bool:

        S = []

        T = []

        for i in range(len(s)):

            if s[i] == "#":

                if S :

                    S.pop()

            else :

                S.append(s[i])

        for i in range(len(t)):

            if t[i] == "#":

                if T :

                    T.pop()

            else :

                T.append(t[i])

        print(S,T)

        if S == T :

            return True

        return False
       # use a function and pass the s, t 
```


### [977. Squares of a Sorted Array](https://leetcode.com/problems/squares-of-a-sorted-array/) 

```python 
class Solution:

    def sortedSquares(self, nums: List[int]) -> List[int]:

        left = 0

        right = len(nums)-1

        idx = len(nums)-1

        res = [0] * len(nums)

        while (left <= right):

            if abs(nums[left]) > abs(nums[right]):

                res[idx ] = nums[left] * nums[left]

                left = left+1

            else :

                res[idx ] = nums[right] * nums[right]

                right = right -1

            idx -= 1

        print(res )

        return res
```

### [8. String to Integer (atoi)](https://leetcode.com/problems/string-to-integer-atoi/)


```python 

class Solution:

    def myAtoi(self, s: str) -> int:

        INT_MAX =2**31-1

        INT_MIN = -2**31

        dd = s.lstrip() #use the var and do the strip ()

        Sign = False

        if len(dd) == 0 :

            return 0

        if dd[0] in ["-","+"]:

            if dd[0] =="-":

                Sign = True

                dd = dd[1:]

            elif dd[0] == "+":

                Sign = False

                dd = dd[1:]

        res = ""

        for i in dd:

            if not  i.isdigit():

                break

            res = res+ i

        if len(res) == 0 :

            return 0

        num = int(res)

        if Sign :

            num = -num

        if num >  INT_MAX :

            num = INT_MAX

        if num < INT_MIN:

            num = INT_MIN

        return num
```

### [373. Find K Pairs with Smallest Sums](https://leetcode.com/problems/find-k-pairs-with-smallest-sums/)


Brute Force : 

TC - > (O(K² + K log K))

Throws the Memory Limit Exceeded 

```python 
class Solution:

    def kSmallestPairs(self, nums1: List[int], nums2: List[int], k: int) -> List[List[int]]:

        dd = []

        for i in range(len(nums1)):

            for j in range(len(nums2)):

                dk  = [nums1[i],nums2[j] ]

                dd.append((dk))

        Sort = sorted(dd  , key = lambda  x : x[0] + x[1] )

        return Sort[:k]
```

