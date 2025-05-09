
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
===============================
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

### [378. Kth Smallest Element in a Sorted Matrix](https://leetcode.com/problems/kth-smallest-element-in-a-sorted-matrix/)

	TC -> O(N^2 NlogN)

```python 
class Solution:

    def kthSmallest(self, matrix: List[List[int]], k: int) -> int:

        dd = []

        for i in range(len(matrix)):

            for j in range(len(matrix[0])):

                dd.append(matrix[i][j])

        dk = sorted(dd)

        return dk[k-1]
```


### [347. Top K Frequent Elements](https://leetcode.com/problems/top-k-frequent-elements/)

TC  -> O(N LogN )


```python 
class Solution:

    def topKFrequent(self, nums: List[int], k: int) -> List[int]:

        dd = {}

        for i in range(len(nums)):

            if nums[i] not in dd :

                dd[nums[i]] = 1

            else :

                dd[nums[i]] += 1

        dk  = sorted(dd.items() , key = lambda x : x [1] , reverse = True)

        count =  0

        res = []

        for i in range(len(dk)):

            count += 1

            if count == k+1 :

                break

            res.append(dk[i][0])

        return res
```

Using the Heap : 

TC -> O(N log K )

```python 
class Solution:

    def topKFrequent(self, nums: List[int], k: int) -> List[int]:

        heap = []

        dd = {}

        for i in range(len(nums)):

            if nums[i] not in dd :

                dd[nums[i]] = 1

            else :

                dd[nums[i]] += 1

        for  idx, val in dd.items():

            heapq.heappush(heap,(val*-1,idx))

        # print(heap)

        ans =[]

        for i in range(k):

            idx, val = heapq.heappop(heap)

            # print(idx,val)

            ans.append(val)

        return ans
```
### [215. Kth Largest Element in an Array](https://leetcode.com/problems/kth-largest-element-in-an-array/)


USING THE HEAP FOR THE O( N LOG K )  BETTER THAN THE SORTING O( N LOG N ): 

TC -> O( N LOG K )
```PYTHON 
class Solution:

    def findKthLargest(self, nums: List[int], k: int) -> int:

        heap = []

        for i in (nums):

            heapq.heappush(heap,i )

            if len(heap)> k :

                heapq.heappop(heap)

        return heap[0]
```


### [451. Sort Characters By Frequency](https://leetcode.com/problems/sort-characters-by-frequency/)

```python 
class Solution:

    def frequencySort(self, s: str) -> str:

        dd = {}

        for i in range(len(s)):

            if s[i] not in dd :

                dd[s[i]] = 1

            else :

                dd[s[i]] +=1

        # print(dd)

        dk = sorted(dd.items(), key = lambda x :  x[1] ,reverse = True )

        # print(dk)

        res = ""

        for i in range(len(dk)):

            Ans = dk[i][0] * dk[i][1]

            # print(res)

            res += Ans

        # print(res)

        return res
```


### [50. Pow(x, n)](https://leetcode.com/problems/powx-n/)



```python 
class Solution:

    def myPow(self, x: float, n: int) -> float:

        res = 1

        if n < 0 : # handle the edge case if the power is a negative

            x   = 1/ x

            n = -n

        while (n > 0 ):

            if n % 2 == 1 :

                res = res * x

            x = x * x

            n = n // 2  # base increse and the exponotial decreses 

        return res
```


### [3. Longest Substring Without Repeating Characters](https://leetcode.com/problems/longest-substring-without-repeating-characters/)

```python 

class Solution:
    def lengthOfLongestSubstring(self, s: str) -> int:
        if len(s) == 0 :return 0 
        if len(s) == 1 :return 1 
        NewString = ""
        count = 0 
        Ans = 0 
        for i in range(len(s)):
            if s[i] not in NewString :
                count = count +  1 
                NewString = NewString + s[i]
            else :
                if count > Ans :
                    Ans = count 
                count = 1 
                index = NewString.index(s[i])
                print("The idx:",index)
                NewString = NewString[index+1:] + s[i]
                print("The NewString :", NewString)
                count = len(NewString)
        if Ans < count :
            Ans = count 
        return Ans 

```


MATH : 
# PRIME 
### Prime Factors

```python 
import math
class Solution:
	def AllPrimeFactors(self, N):
		# Code here
		def isPrime(N :int)->bool :
		    if N <= 1 :return 0 ### not zero 
		    for i in range(2, int(math.sqrt(N))+1):
		        if N % i == 0 :
		            return False 
		    return True
		if isPrime(N):return [N] ## if the input is a prime number 
		dd =  []
		for i in range(2, N):
		    if ((N % i == 0 ) and (isPrime(i))):
		        dd.append(i)
		dk = sorted(dd)
		return dk
```

### Sieve of Eratosthenes

```python 
import math
class Solution:
    def sieveOfEratosthenes(self, N):
		def isPrime(N :int)->bool :
		    if N <= 1 :return 0 ### not zero 
		    for i in range(2, int(math.sqrt(N))+1):
		        if N % i == 0 :
		            return False 
		    return True
		dd =  []
		for i in range(2, N+1):
		    if (isPrime(i)):
		        dd.append(i)
		return dd
```


### [204. Count Primes](https://leetcode.com/problems/count-primes/)

Normal Prime will take more computation when compared to this. 

Core logic :
Is  marking  False if the number is a Multiple of i of the starting loop. 

```python 
class Solution:
    def countPrimes(self, N: int) -> int:
        List = [True] * N
        if N < 2 :
            return 0 
        List[0] = List[1] = False 
        # count =  0 
        # for i in range(2, N): # 
        for i in range(2,int(N**0.5) + 1): # optimized loop  use the int(math.sqrt (N)+ 1) 
            if List[i] :
                # count += 1 
                for j in range(i*i, N , i): # start , end , step we have to step the value
                    List[j] = False 
        return sum(List)

```


### [2521. Distinct Prime Factors of Product of Array](https://leetcode.com/problems/distinct-prime-factors-of-product-of-array/)

TLE : 


```python 
class Solution:
    def distinctPrimeFactors(self, nums: List[int]) -> int:
        Ans = 1
        for i in range(len(nums)):
            Ans = Ans * nums[i]
        # print(Ans)
        def isprime (  N :int ) -> bool :
            if N ==  0 : return False 
            for i in range(2,int(math.sqrt(N))+1):
                if N % i == 0 :
                    return False 
            return True 
        count = 0 
        for i in range(2,Ans+1):
            dk = Ans % i 
            if dk == 0 and isprime(i):
                count += 1
        print(count)
        return count 
```

OPTIMIZED : 

```python 
class Solution:
    def distinctPrimeFactors(self, nums: List[int]) -> int:
        def isprime(N: int) -> bool:
            if N <= 1:
                return False
            for i in range(2, int(math.sqrt(N)) + 1):
                if N % i == 0:
                    return False
            return True

        # Set to store distinct prime factors
        prime_factors = set()

        # Loop through each number in the list
        for num in nums:
            # Check each number for prime factors
            for i in range(2, num + 1):
                if num % i == 0 and isprime(i):
                    prime_factors.add(i)
        
        # Return the number of distinct prime factors
        return len(prime_factors) 

       
```