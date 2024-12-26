
### [69. Sqrt(x)](https://leetcode.com/problems/sqrtx/)

TC -> O(N)

```python 
class Solution:

    def mySqrt(self, x: int) -> int:

        ans = 0  

        if x == 1 :

            return 1

        for i in range(1,x):

            if i*i <= x:

                ans = i  

            else :

                break

        return ans
```

TIME COMPLEXITY : O( N LOG N )

```PYTHON 
class Solution:

    def mySqrt(self, x: int) -> int:

        ans = 0

        left =  1

        right = x  

        while (left <= right):

            mid = left + (right-left) // 2

            if mid * mid <= x :

                ans  = mid

                left =mid + 1

            else :

                right = mid -1

        return ans
```


###   Find Nth Root Of M

TC => O (LOG M)

```python

def NthRoot(n: int, m: int) -> int:

    root = m**(1/n)

    if round(root) **(n) ==m :

        return int(round(root)) 

    else :

        return -1
```



### [875. Koko Eating Bananas](https://leetcode.com/problems/koko-eating-bananas/)

```PYTHON 
class Solution:

    def minEatingSpeed(self, piles: List[int], h: int) -> int:

        left = 1  # Minimum possible eating speed

        right = max(piles)  # Maximum possible eating speed

        def ischeck(piles, mid):

            Sum = 0

            for i in piles:

                Sum += math.ceil(i / mid)  # Calculate hours required for each pile

            return Sum

  

        ans = -1

        while left <= right:

            mid = left + (right - left) // 2

            if ischeck(piles, mid) <= h:  # Check if current speed is valid

                ans = mid  # Store the current valid speed

                right = mid - 1  # Try smaller speeds

            else:

                left = mid + 1  # Try larger speeds

        return ans
       
```


