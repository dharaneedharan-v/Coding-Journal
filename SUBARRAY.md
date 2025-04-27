# HINT : 

## *To iterate in O(N) ==> Use the hash Map or the Prefixsum to Eliminate the N^ 2 or N ^ 3*

## *If it is a subarray sum means you can strightly go for the perfix sum and hash Map for the efficient solution*

## *You can  also use the Set to eliminate the Time Complexity also Depends on the problems also....*

=========================================================

### [560. Subarray Sum Equals K](https://leetcode.com/problems/subarray-sum-equals-k/)


Time Limit Exceeded  : 


```python 

class Solution:

    def subarraySum(self, nums: List[int], k: int) -> int:

        count = 0

        for i in range(len(nums)):

            for  j in range(i+1,len(nums)+1):  #i+1 is used because to eliminate the empty subarray

                dk = sum(nums[i:j])

                if dk == k :

                    count += 1

        return count
```




TC -> O(N) and SC - > O(N)

```python 
class Solution:
    def subarraySum(self, nums: List[int], k: int) -> int:
        dd = {}
        count = 0 
        Sum = 0 
        for i in range(len(nums)):
            Sum = Sum + nums[i]
            if Sum == k :
                count += 1
            if Sum - k in dd :
                count += dd[Sum - k]
            dd[Sum] = dd.get(Sum,0)+1 
        return count    
```


### [523. Continuous Subarray Sum](https://leetcode.com/problems/continuous-subarray-sum/)

Time Limit Exceeded  : 

```python 
class Solution:

    def checkSubarraySum(self, nums: List[int], k: int) -> bool:

        for i in range(len(nums)):

            for j in range(i+1,len(nums)):

                dk  = sum(nums[i:j+1])

                if dk == 0 and k == 0 :

                    return True

                if k != 0 and dk % k  ==0 :

                    return True

        return False
```


TC -> O(N), SC -> O(N)

```python 
class Solution:

    def checkSubarraySum(self, nums: List[int], k: int) -> bool:

        dd = {}

        Sum = 0

        for i in range(len(nums)):

            Sum = (Sum + nums[i] )% k

            if Sum  == 0 and i>= 1 : #special case want to handle it  or otherwise inizitalized it in the dict starting itself

                return  True

            if Sum in dd :

                if i-dd[Sum] > 1 : # Not 2

                    return True

            else :

                dd[Sum] = i

        return False
```


```python 
class Solution:

    def checkSubarraySum(self, nums: List[int], k: int) -> bool:

        dd  =  set ()

        Sum = 0

        Last = 0

        for i in range(len(nums)):

            Sum  = (Sum + nums[i]) % k

            if Sum in dd :

                return True

            else :

                dd.add(Last )

                Last = Sum

        return False
```