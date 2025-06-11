
Striver : -> Hard 

### [921. Minimum Add to Make Parentheses Valid](https://leetcode.com/problems/minimum-add-to-make-parentheses-valid/)


```python 
class Solution:
    def minAddToMakeValid(self, s: str) -> int:
        count = 0 
        close  = 0 
        for i in s :
            if i == "(":
                count +=  1 
            else :
                if count > 0 : 
                    count -= 1 
                else :
                    close += 1 
        return close + count 


```


### [38. Count and Say](https://leetcode.com/problems/count-and-say/)


```python 
class Solution:
    def countAndSay(self, n: int) -> str:
        def Count(N):
            dd =[]
            dk = str(N)
            count = 1
            for i in range(1,len(dk)):
                if dk[i-1] == dk[i]:
                    count +=1 
                else :
                    dd.append(str(count))
                    dd.append(dk[i-1])
                    count = 1 
            dd.append(str(count)) # We have to update the last group
            dd.append(dk[-1]) # Last element 
            return "".join(dd)
        dd = "1"
        for i in range(n-1):
            See = Count(dd)
            dd = See 
            print(See)
        return dd 
```


