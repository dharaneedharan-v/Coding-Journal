


### Find length of the longest subarray containing atmost two distinct integers

 TC - > O(N^2)
````PYTHON 

class Solution:
    def totalElements(self,arr):
        # Code here
        Max = 0 
        if len(arr) == 1 :
            return 1
            
        for i in range(len(arr)):
            dd = set()
            for j in range(i,len(arr)):
                dd.add(arr[j])
                if len(dd)> 2:
                    break
                if len(dd) == 2 : 
                    Max = max(Max , j-i+1) # for the lenght update 
                # break
        return Max
```

