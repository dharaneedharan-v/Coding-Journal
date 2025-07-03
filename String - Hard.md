
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


### Challenge by Nikitasha

TLE : 

```python 

#User function Template for python3
class Solution:
    MOD = 1e9+7
    def MaxLength(self ,  String):
        Sum = 0 
        j = 0 
        for i in range(len(String)):
            Sum += ( ord(String[i])* (k**j ))%int(self.MOD)
            j += 1 
        return Sum % int(self.MOD)
        
    def Substrings(self , Str , Z):
        Len = len(Str)
        List = []
        for i in range(Len-Z+1):
            List.append(Str[i:i+Z])
        return List
        
        
    def findMaximum (self, N, Z, K,S):
        SubString = list(self.Substrings(S , Z))
        # print(SubString)
        
        Max = []
        for i in SubString :
            Max.append(self.MaxLength(i) ) 
        Ans = (max(Max))

        return Ans
            
                
```