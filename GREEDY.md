
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