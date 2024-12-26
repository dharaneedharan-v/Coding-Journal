
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