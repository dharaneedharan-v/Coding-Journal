
# MEDIUM

###  Print Maximum Sub Array

```python 
#User function Template for python3

class Solution:
    # Function to find the subarray with the maximum sum
    def findSubarray(self, arr):
    	# code here
    	Max = -1  
    	Res = []
    	for i in range(len(arr)):
    	    Sum = 0 
    	    EMpty = []
    	    for j in range(i+1, len(arr)+1):
    	        if arr[j-1] < 0 :
    	            break 
    	        else :
    	            Sum += arr[j-1]
    	            EMpty.append(arr[j-1])
    	    if Max < Sum :
    	        Max = Sum
    	        Res = EMpty
    	return Res if len(Res) !=  0  else [-1]
```


### [31. Next Permutation](https://leetcode.com/problems/next-permutation/)

```python 

class Solution:
    def nextPermutation(self, nums: List[int]) -> None:
        """
        Do not return anything, modify nums in-place instead.
        """
        idx = -1
        for i in range(len(nums)-2,  -1 , -1 ):
            if nums[i] < nums[i+1]:
                idx = i
                break 
        print(idx)
        if idx == -1 :
            nums.reverse()
            return 
            # return reversed(nums)
        else:
            pass
        for i in range(len(nums)-1 , idx, -1 ):
            if nums[i] > nums[idx]:
                nums[i] , nums[idx] = nums[idx]   , nums[i]
                break 
        nums[ idx+1 : ] = reversed(nums[ idx+1 : ])
    
```

### Longest Consecutive Subsequence : 

```python 
 #User function Template for python3
 
class Solution:
    
    # arr[] : the input array
    
    #Function to return length of longest subsequence of consecutive integers.
    def longestConsecutive(self,arr):
        #code here
        Set = sorted(set(arr))  # This is slightly more efficient
        count = 1 
        Max = 1  
        for i in range(1, len(Set)):
            if Set[i-1] == Set[i]-1:
                count += 1 
                Max = max(count , Max)
            else :
                count = 1 
        return Max  
```




###  [560. Subarray Sum Equals K](https://leetcode.com/problems/subarray-sum-equals-k/)

TLE 
BRUTE : 
HINT :  Optimized Means Go for the Prefix and the HashMap..  
```python 
class Solution:
    def subarraySum(self, nums: List[int], k: int) -> int:
        Max = -1 
        count = 0 
        for i in range(len(nums)):
            Sum = 0 
            for j in range(i + 1 , len(nums)+1):
                Sum += nums[j-1]
                if Sum  == k :
                    count += 1 
        return count 
        
```


### [48. Rotate Image](https://leetcode.com/problems/rotate-image/)

```python 
class Solution:
    def rotate(self, matrix: List[List[int]]) -> None:
        """
        Do not return anything, modify matrix in-place instead.
        """
        Transpose =[]
        Row =  len(matrix)
        Col =  len(matrix[0])
       
        for i in range(Col):
            New = []
            for j in range((Row)):
                New.append(matrix[j][i])
            Transpose.append(New)
        # print(Transpose)

        def Rev(Nums):
            Res = []
            for i in range(len(Nums)-1, -1, -1):
                Res.append(Nums[i])
            return Res
                 
        for i in range(len(Transpose)):
            Transpose[i] = Rev(Transpose[i])
        # print(Transpose)
        matrix [:] = Transpose

```


# HARD :


### [118. Pascal's Triangle](https://leetcode.com/problems/pascals-triangle/)

```python 
class Solution:
    def generate(self, nums: int) -> List[List[int]]:
        if nums ==0 :
            return []
        if nums == 1 :
            return [[1]]
        Res = [[1]]
        for i in range(1 , nums ):
            pre = Res[-1]
            New = [1] ################ As the pascal Triangle Follows the First Strats Witht the 1 Alaways
            for j in range(1 , i ):
                New.append(pre[j-1] + pre[j])
            New.append(1) ###################As the pascal Triangle ALways Ends Witht the 1 
            Res.append(New)
        print(Res)
        return Res 
```


### [119. Pascal's Triangle II](https://leetcode.com/problems/pascals-triangle-ii/)


```python 
class Solution:
    def getRow(self, nums: int) -> List[int]:
        if nums == 0 :
            return [1]
        Res  = [[1]]
        for i in range(1, nums+1):
            New = [1]
            pre = Res[-1]
            for j in range( 1 , i ):
                New.append(pre[j-1] +  pre[j])
            New.append(1)
            Res.append(New)
        return Res[-1]
```

### [229. Majority Element II](https://leetcode.com/problems/majority-element-ii/)

```python 
class Solution:
    def majorityElement(self, nums: List[int]) -> List[int]:
        Find = len(nums)// 3 ### First FInd the HOw many Elements are there Then Proceed it... 
        print(Find)
        Map = {}
        for  i  in range(len(nums)):
            if nums[i] not in Map :
                Map[nums[i]] = 1
            else :
                Map[nums[i]] += 1 
        # print(Map)
        Res = []
        for idx , val in Map.items():
            if val < Find :
                Res.append(idx)
        print(Res)
        return Res  
```


### Largest subarray with 0 sum


```python 
class Solution:
    def maxLength(self, arr):
        # code here
        Max = 0 
        for i in range(len(arr)):
            Sum = 0 
            Count = 0 
            for j in range(i+1 , len(arr)+1):
                Sum += arr[j-1]
                Count +=  1 
                if Sum == 0 :
                    Max = max(Count , Max)
        # print(Max )
        return Max 

        
```


### Count Subarrays with given XOR

TLE : 

```python 
class Solution:
    def subarrayXor(self, arr, k):
        # code here
        Max = 0 
        for i in range(len(arr)):
            Sum  = 0 
            for j in range(i+1 , len(arr)+1):
                # print(arr[i:j])
                Sum ^= arr[j-1]
                if Sum == k :
                    # print(arr[i:j] , Sum)
                    Max += 1 
        # print(Max)
        return Max 
            
```


### [56. Merge Intervals](https://leetcode.com/problems/merge-intervals/)

```python 
class Solution:
    def merge(self, nums: List[List[int]]) -> List[List[int]]:
        nums.sort()
        Res = [nums[0]]
        for i in range(len(nums)):
            Start , End = Res[-1]
            if End >= nums[i][0]:
                Res[-1][1] = max(End , nums[i][1])
            else :
                Res.append(nums[i])
        return Res 


```

### [2965. Find Missing and Repeated Values](https://leetcode.com/problems/find-missing-and-repeated-values/)


```python 
class Solution:
    def findMissingAndRepeatedValues(self, grid: List[List[int]]) -> List[int]:
        lists = []
        for i in range(len(grid)):
            for j in grid[i]:
                lists.append(j)
        Number = 0 

        lists.sort()
        for i in range(1, len(lists)):
            if lists[i] == lists[i-1]:
                Number = lists[i]
                break 
        dk = [ i for i  in range(1,len(lists)+1)]
        print(dk)
        Res = -1
        for i in range(len(dk)):
            if dk[i] not  in lists:
                Res = dk[i] 
        return [Number,Res]

```


### [88. Merge Sorted Array](https://leetcode.com/problems/merge-sorted-array/)


Not optimal, Interviewer Not accept this Solution... 

```python 
class Solution:
    def merge(self, nums1: List[int], m: int, nums2: List[int], n: int) -> None:
        """
        Do not return anything, modify nums1 in-place instead.
        """
        Res = []
        for i in range((m)): 
            Res.append(nums1[i])
        for i in range((n)):
            Res.append(nums2[i])
        Res.sort()
        # nums1 [:] = Res  ###  or  USing the Loop..  
        for i in range(n+m):
            nums1[i] = Res[i] 
        
```


