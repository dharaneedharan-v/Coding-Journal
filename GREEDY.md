
### Minimum number of Coins

```python 
#User function Template for python3

class Solution:
    def minPartition(self, N):
        # code here
        Res = []
        Map = [1 ,2 , 5, 10, 20, 50, 100, 200, 500, 2000]
        for i in range(len(Map)-1 , -1 , -1 ):
            while  N >=Map[i]: #### NOT N == Map[i] == 0 :   we want tp check the if the Numbe Number is greater than the current element.. While isused insted of IF if there are more than the same element .
                Res.append(Map[i])
                N = N-Map[i]
        return Res
                
```


### [860. Lemonade Change](https://leetcode.com/problems/lemonade-change/)


```python 
class Solution:
    def lemonadeChange(self, bills: List[int]) -> bool:
        count5 = count10 = count20 = 0 
        for i in range(len(bills)):
            if bills[i] == 5 :
                count5 += 1 
            elif  bills[i] == 10 :
                if count5 == 0 :
                    return False 
                else:
                    count10 += 1 
                    count5 -= 1 
            else :
                if count5 > 0 and count10 > 0 :
                    count10 -= 1
                    count5 -= 1
                elif count5 >= 3 : ### Must be equal IMPORTANT 
                    count5 -= 3
                else :
                    return False 
        return True 
                
```


### [678. Valid Parenthesis String](https://leetcode.com/problems/valid-parenthesis-string/)

```python 
class Solution:
    def checkValidString(self, s: str) -> bool:
        Open = 0 
        Close = 0 
        for i in range(len(s)):
            if s[i] == "(":
                Open += 1
                Close += 1
            if s[i] == ")":
                Open -= 1 
                Close -= 1
            if s[i] == "*":
                Open += 1
                Close -= 1 
            if (Open < 0 ):
                return False 
            Close= max(0 , Open)
        return Close == 0 
                
```

### N meetings in one room

```python 
#User function Template for python3

class Solution:
    
    #Function to find the maximum number of meetings that can
    #be performed in a meeting room.
    def maximumMeetings(self,start,end):
        # code here
        List = []
        for i in range(len(start)):
            List.append((start[i] , end[i]))
            # print(start[i] , end[i])
        # print(List)
        List.sort(key = lambda x: x[1])
        # print(List)
        Count = 0 
        LastEndTime = -1 # Not the 0 if the Start Time is zero means we will be losing the Coun of the One meeting... 
        
        for i in range(len(List)):
            
            Start , End = List[i]
            # print(Start , End)
            if Start  > LastEndTime: 
                Count += 1
                LastEndTime = End 
        # print(Count)
        return Count 

```


### [55. Jump Game](https://leetcode.com/problems/jump-game/)

```python 

class Solution:
    def canJump(self, nums: List[int]) -> bool:
        if len(nums)==  1: return True  # Single Edge Case...
        MaxSteps = nums[0] 
        for i in range(len(nums)):
            MaxSteps -= 1 # Reduce one by one
            if MaxSteps < 0 : return False   # Maxsteps goes negative Not possible to Move ,if the zero encounters we can able to move also....
            if MaxSteps == len(nums)-1 : return True  # check for the Any Max steps also possible or not While going or taking instead of one steps... 
            if MaxSteps < nums[i]:
                MaxSteps  = nums[i]
        return True # To tell fuction it can reach the end and return True... 
        
```

### [45. Jump Game II](https://leetcode.com/problems/jump-game-ii/)

```python 
class Solution:
    def jump(self, nums: List[int]) -> int:
        Start = End = Count = 0 
        for i in range(len(nums)-1):
        # Update the Start First 
            Start = max(Start , nums[i]+i)
        # Update the End if i == End as the Start 
            if i == End  :
                Count += 1 
                End = Start 
        return Count 
```



### [56. Merge Intervals](https://leetcode.com/problems/merge-intervals/) 

```python 
class Solution:
    def merge(self, intervals: List[List[int]]) -> List[List[int]]:
        if len(intervals)== 1 :
            return intervals
        intervals.sort(key=lambda x : x[0]) #####
        # print(intervals)
        dk = [intervals[0]]
        for i in range(len(intervals)):
            Start , End  = dk[-1]
            # print(Start , End )
            if End  >= intervals[i][0] :
                dk[-1][1] = max(End , intervals[i][1] )
            else :
                dk.append(intervals[i])
        # print(dk)
        return dk 
```


### [57. Insert Interval](https://leetcode.com/problems/insert-interval/)


```python 
class Solution:
    def insert(self, intervals: List[List[int]], newInterval: List[int]) -> List[List[int]]:
        intervals.append(newInterval)
        if len(intervals)== 1 :
            return intervals
        intervals.sort(key=lambda x : x[0])
        # print(intervals)
        dk = [intervals[0]]
        for i in range(len(intervals)):
            Start , End  = dk[-1]
            # print(Start , End )
            if End  >= intervals[i][0] :
                dk[-1][1] = max(End , intervals[i][1] )
            else :
                dk.append(intervals[i])
        # print(dk)
        
        return dk  
        
```


### [435. Non-overlapping Intervals](https://leetcode.com/problems/non-overlapping-intervals/)


```python 
class Solution:
    def eraseOverlapIntervals(self, intervals: List[List[int]]) -> int:
        intervals.sort(key  = lambda x : x[0])
        count = 0 
        Min_End_Track = intervals[0][1] # To Track the Overlapping Intervals or Preview Intervals
        for i in range(len(intervals)):
            Start , End = intervals[i]
            if Min_End_Track > Start :
                count += 1 
                Min_End_Track = min(Min_End_Track, End) # To keep Track of the Overlapping Intervals
            else :
                Min_End_Track = End  # If No Overlapping Itervals Found Then Update the Min_End_Track as End.....
        return count -1 
    
```



#  Job Sequencing Problem

```PYTHON 
from os import *
from sys import *
from collections import *
from math import *

def jobScheduling(jobs):
    Jobs = TotalAmount = 0 
    # print(jobs)
    jobs.sort(key=lambda x: x[2], reverse=True)    
    Max = max( i[1] for i in jobs)
    # print(Max)
    HashArr = [-1] *( Max+1 ) 
    # print(HashArr)
    for i in range(len(jobs)):
        idx , deadline , Amount = jobs[i]
        for j in range(deadline ,  0 , -1):
            if HashArr[j] == -1:
                HashArr[j] = idx 
                TotalAmount+= Amount
                Jobs+= 1
                break 
    return [Jobs , TotalAmount ]

```


### Page Faults in LRU

```python 
#User function Template for python3
from collections import deque
class Solution:
    def pageFaults(self, N, C, pages):
        count = 0 
        dk  = [-1]*C
        Stack = deque(dk)
        for i in range(len(pages)):
            if pages[i] not in Stack :
                count +=1 
                if len(Stack) == C :
                    Stack.popleft()
                Stack.append(pages[i])
            else : # If the Elelment ALready present in the Stack Means We want to take the elelment and Add it to the first.. 
                Stack.remove(pages[i])
                Stack.append(pages[i])
        return count 
        
        
```



### Minimum Platforms

TLE : 

```python 
class Solution:
    def minimumPlatform(self, arr, dep):
        max_platforms = 0
        for time in range(0, 2360):  # total 2360 iterations
            count = 0
            for i in range(len(arr)):
                if arr[i] <= time <= dep[i]:
                    count += 1
            max_platforms = max(max_platforms, count)
        return max_platforms
```

Optimal : 


```python 
Minimum Platforms
#User function Template for python3

class Solution:    
    #Function to find the minimum number of platforms required at the
    #railway station such that no train waits.
    def minimumPlatform(self,arr,dep):
        # code here
        arr.sort()
        dep.sort()
        ln  = len(arr)
        i = j = 0 
        count =  0 
        MaxPlatform = 0 
        while  i < ln and j < ln :
            if arr[i] <= dep[j]:
                count += 1 
                i+= 1
            else :
                count -=  1 
                j += 1
            MaxPlatform = max(MaxPlatform , count )
        return MaxPlatform 
            
```


### [455. Assign Cookies](https://leetcode.com/problems/assign-cookies/)

```python 
class Solution:
    def findContentChildren(self, g: List[int], s: List[int]) -> int:
        g.sort()
        s.sort() 
        count = 0
        i = j = 0 
        while i  < len(g) and j < len(s) :
            if s[j] >= g[i]:
                count += 1
                i += 1 # condtoion satisified , Next Move the Child 
            j+= 1 ## if not Next cookie 
        return count 
```