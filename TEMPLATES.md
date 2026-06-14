### *SLIDING WINDOW :* 

*FOR THE FIXED WINDOW SIZE  :  LIKE WHEN THE SIZE OF THE ARRAY AND THE WINDOW IS K IS CONSTANT* 

*ITERATION : **

```PYTHON 
n = len(arr)
for i in range(n-k+1 ):
print(arr[i:i+k])
```


### *Sliding Window Template (print window elements):  Slicing the element*  

```python 
def sliding_window(arr, k):
    n = len(arr)
    for i in range(n - k + 1):
        window = arr[i:i+k]  # get current window
        print(window)

# Example usage
arr = [2, 1, 5, 1, 3, 2]
k = 3
sliding_window(arr, k)

```

*output* 
```output 
[2, 1, 5]
[1, 5, 1]
[5, 1, 3]
[1, 3, 2]

```


# *Slightly *faster* version (avoiding slicing)*

```python 
def sliding_window(arr, k):
    n = len(arr)
    window = []
    
    # build first window
    for i in range(k):
        window.append(arr[i])
    print(window)   
    # print upto the window size. if k = 3 means , 
    #   // Output is [2, 1, 5] 

    # slide the window
    for i in range(k, n):
        window.pop(0)
        window.append(arr[i])
        print(window)

# This part is used to pop the first element of the window and append the new elemnt to the window. 

# Example usage
arr = [2, 1, 5, 1, 3, 2]
k = 3
sliding_window(arr, k)

```


| Version            | Method                          | Speed                       | Notes                                                            |
| ------------------ | ------------------------------- | --------------------------- | ---------------------------------------------------------------- |
| **First version**  | Uses slicing (`arr[i:i+k]`)     | **Slower**                  | Every slice creates a **new list** every time.                   |
| **Second version** | Manual sliding (pop and append) | **Faster** (for big inputs) | Only modifies the same list (no copy) — better for large arrays. |
*Tip :*

*Use  the deque for the faster pop operations.* 

***Best practice for maximum speed:***  

*✅ *Use `collections.deque`* — popping from the front is fast (`O(1)`).*

```python 
from collections import deque

def sliding_window(arr, k):
    n = len(arr)
    window = deque()

    # build first window
    for i in range(k):
        window.append(arr[i])
    print(list(window))

    # slide the window
    for i in range(k, n):
        window.popleft()
        window.append(arr[i])
        print(list(window))

# Example usage
arr = [2, 1, 5, 1, 3, 2]
k = 3
sliding_window(arr, k)

```
*output:* 
```python 
[2, 1, 5]
[1, 5, 1]
[5, 1, 3]
[1, 3, 2]
```

*🚀 *This is the fastest*, because:*

- *`deque.popleft()` is *O(1)*.*
    
- *`deque.append()` is *O(1)*.*
    
- *No list slicing.*



### *Consecutive Number :* 

*For a Fixed Sizes :  K = 3 :* 
### *This is a classic sliding window:*
*Templates*  
```python 
for i in range(len(arr) - 2):
    print(arr[i], arr[i+1], arr[i+2])
```

### *Generalized Sliding Window:*

```python 
window_size = 3
for i in range(len(arr) - window_size + 1):
    print(arr[i:i + window_size])

```

### *Combinations :* 

```python 
for i in range(len(arr)):
    for j in range(i+1, len(arr)):
        for k in range(j+1, len(arr)):
            print(arr[i], arr[j], arr[k])
```


*Output :* 

```python 
arr = [1, 2, 3, 4]

# Output:
1 2 3
1 2 4
1 3 4
2 3 4

```

*Using the Build In :*

```python 
from itertools import combinations

for a, b, c in combinations(arr, 3):
    print(a, b, c)

```


*Recursion :*


*https://www.youtube.com/watch?v=gPh-TDr68ao&list=PLKBtxy4DjJ0PbAq0FfT_fySebT4DOpCV1&index=2*




*-----*


#### *DICTIONARY :* 
*NOTES*
	*In the dictionary Negative indexing is not possible...*

*Basic : To Access it *  

```python 
Map = {}
        for  i  in range(len(nums)):
            if nums[i] not in Map :
                Map[nums[i]] = 1
            else :
                Map[nums[i]] += 1 
        # print(Map)
```


Forming the Key and Values From the different Sources, 

```python 
keys = ["a", "b", "c"]
values = [1, 2, 3]

d = dict(zip(keys, values))
print(d)

# {'a': 1, 'b': 2, 'c': 3}
```


Auto idx value for the Index value 


```python 
items = ["apple", "banana", "orange"]

d = {i: item for i, item in enumerate(items)}
print(d)
# {0: 'apple', 1: 'banana', 2: 'orange'}
```

----
### *TWO POINTER*

*NOTES*: 
- HI 

Using the While Loop.
```python 
data = [3, 4, 2, 1]

left = 0
right = len(data) - 1

while left < right:
    print(data[left], data[right])
    left += 1
    right -= 1
```


Using the For Loop : 

```python 
for i in range(len(data) // 2):
    print(data[i], data[len(data) - 1 - i])
```



---

### *LINKED LIST* :

*NOTES:*
- *TRAVERSING* 

*For Traversing : Simple Approach..* 

```python 
temp = head

        data = []

        while temp :

            data.append(temp.val) ## Important Use the Val Not Next if you use the .Next  it will return the head of the next node.

            temp  = temp.next

        print (data)
```