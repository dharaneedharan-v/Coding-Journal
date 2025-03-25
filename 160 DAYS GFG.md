
### 1. Second Largest

```PYTHON 
class Solution:
    def getSecondLargest(self, arr):
        First =  -1
        Second = -1 
        for i in range(len(arr)):
            if arr[i] > First :
                Second = First 
                First = arr[i]
            elif arr[i] >  Second and arr[i] < First :
                Second = arr[i]
        return Second 
```

### 2. Move All Zeroes to End

```python 

class Solution:
	def pushZerosToEnd(self,arr):
	    count = 0 
	    for i in  range(len(arr)):
	        if arr[i] != 0 :
	            arr[count] , arr[i] = arr[i] , arr[count]
	            count += 1 
```


