
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


### 3. Reverse an Array

 Using the left and right pointer , And inplace modify it.
 
```python 


class Solution:

    def reverseArray(self, arr):

        left  =  0 

        right = len(arr)-1

        while left < right :

            arr[left], arr[right] = arr[right] , arr[left]

            left = left + 1

            right = right -1

        return arr

```
