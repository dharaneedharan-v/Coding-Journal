
### ✅ What is a **subsequence**?

A **subsequence** is a part of a list or string where:

- You **keep the original order**
    
- You can **skip some elements**, but you **can’t rearrange** them
    

---

### 🧠 Think of it like this:

You’re **picking some items** from a list, going **left to right**, and you can skip if you want — but you **can’t go back** or change the order.

---

### 📘 Example:

List: `[1, 2, 3]`  
Subsequences:

- `[1]` ✅
    
- `[2]` ✅
    
- `[1, 3]` ✅ (skip 2)
    
- `[1, 2, 3]` ✅ (take all)
    
- `[2, 1]` ❌ (wrong order — not allowed)


---

### 💡 In the context of **subsequences**:

The **empty string** (or empty list `[]`) is always considered a **valid subsequence** of any string or list.

#### Example:

Original string: `"abc"`  
All subsequences include:

- `"a"`
    
- `"b"`
    
- `"c"`
    
- `"ab"`
    
- `"ac"`
    
- `"bc"`
    
- `"abc"`
    
- `""` ← this is the **empty string** ✅

---

## 🤔 Why is **recursion** used for **subsequences** problems?

### ✅ Short Answer:

Because subsequences are naturally about **making a choice at each step** (include or exclude an element), and **recursion handles repeated choices** very well.

---

## 🔍 Let’s dig in step-by-step:

### 🔁 1. **Why not loops only?**

You **can** use loops, but:

- Loops are good when you know the exact steps (e.g., print all elements, move through an array)
    
- But with subsequences, the number of possibilities is **`2^n`**, and you need to explore **all combinations of choices**
    
- Writing that using nested loops becomes **messy and hard to scale**
    

**Example**: For 3 elements → 8 subsequences  
For 10 elements → 1024 subsequences  
How many loops will you write? That’s why **recursion** is easier.

---

### 🧠 2. **Why recursion fits naturally**

Each element in the array or string has **two choices**:

1. Include it in the current subsequence
    
2. Exclude it
    

This “branching” is perfect for recursion.

Here’s how it works:

```python 

def generate_subsequences(arr, index=0, path=[]):
    if index == len(arr):
        print(path)
        return
    
    # Exclude current element
    generate_subsequences(arr, index + 1, path)
    
    # Include current element
    generate_subsequences(arr, index + 1, path + [arr[index]])


```



At each step, recursion:

- Tries the “no” path (skip element)
    
- Tries the “yes” path (include element)
    
- Keeps branching until all choices are explored





### ✅ Task: Generate all subsequences of `[1, 2, 3]`

---

## 🔁 **Using Loops (Hard to Scale)**

Here’s how you'd write this with loops **just for 3 elements**:

```python 
arr = [1, 2, 3]
n = len(arr)

# Brute-force with nested loops
print([])  # empty subsequence
for i in range(n):
    print([arr[i]])
    for j in range(i + 1, n):
        print([arr[i], arr[j]])
        for k in range(j + 1, n):
            print([arr[i], arr[j], arr[k]])

```


### 😵 Problems with this:

- You had to use **3 nested loops**
    
- It only works for 3 elements — imagine writing this for 10 elements (you'd need 10 nested loops!)
    
- Very hard to maintain, debug, and scale
    

---

## 🔁 Same Task: ✅ **Using Recursion (Scalable & Clean)** 

```python 

def subsequences(arr, index=0, path=[]):
    if index == len(arr):
        print(path)
        return
    # Exclude current element
    subsequences(arr, index + 1, path)
    # Include current element
    subsequences(arr, index + 1, path + [arr[index]])

arr = [1, 2, 3]
subsequences(arr)

```
### ✅ Output:

python 

```python 
[]
[3]
[2]
[2, 3]
[1]
[1, 3]
[1, 2]
[1, 2, 3]

```

### ✅ Why this is better:

- Works for **any size** of input
    
- Clean, readable, and logical: **include or exclude**
    
- Scales to 10, 15+ elements without extra code
    
- **Foundation for DP and backtracking**
    

---

### 📦 Final Thought:

Writing `2^n` combinations using loops becomes messy very fast. But recursion handles "include/exclude" choices neatly — that's why it's **preferred** for generating subsequences.

Let me know if you want to try a version that returns the list instead of printing it!


----


✅ **How to calculate the number of subsequences**


``` 
Number of subsequences = 2^n

```


## Want to **exclude the empty subsequence**?

If you only want **non-empty** subsequences:

```
Total = 2^n - 1
```

---

## 🧮 How to calculate in Python:

```python 
n = len([1, 2, 3])
print(2 ** n)         # Total subsequences (including empty)
print(2 ** n - 1)     # Non-empty subsequences

```

===============================================================
***PROBLEMS ON SUBSEQUENCES***

===============================================================

# TEMPLATES: 


```python 

class Solution:
    def __init__(Fuck, A):
        Fuck.A = A
    def REC(Fuck , Nidx , Mlist):
        if Nidx == len(Fuck.A):
            print(Mlist)
            return 
        Fuck.REC(Nidx+1 , Mlist)
        Fuck.REC(Nidx+1 ,Mlist+Fuck.A[Nidx])
if __name__ == "__main__":
    a = input()
    A = Solution(a)
    A.REC(0,"")
```


```python 

def REC( Nidx , Mlist):
    if Nidx == len(A):
        print(Mlist)
        return 
    REC(Nidx+1 , Mlist)
    REC(Nidx+1 ,Mlist+A[Nidx])

A = input()
REC(0,"")

```

```python 
class Solution:
    def generateSubsequences(self, a):
        def helper(idx, path):
            if idx == len(a):
                print(path)
                return
            helper(idx + 1, path)
            helper(idx + 1, path + a[idx])
        helper(0, "")
# Usage
a = input()
sol = Solution()
sol.generateSubsequences(a)
```

===============================================================


### Check if there exists a subsequence with sum K


```python 
class Solution:
    def checkSubsequenceSum(self, N, arr, K):

        def REC(index, curr_sum):
            if index == N:
                return curr_sum == K #######

            if curr_sum > K:  ########
                return False  #########

            if REC(index + 1, curr_sum + arr[index]):
                return True

            if REC(index + 1, curr_sum):
                return True

            return False

        return REC(0, 0)
```



### Sum Subsequences that Are Equal to the  K :

```python 
class Solution:
    # Count = 0 
    def numSubseq(self, nums: List[int], target: int) -> int:
        self.Count = 0 
        def REC( idx , Total):
            if idx == len(nums):
                if Total == target :
                    self.Count +=1 
                    # print(self.Count)
                # print(Total)
                return 
            REC(idx+1,Total)
            REC(idx+1,Total+nums[idx])
        # COUNT = 0 
        REC(0,0)
        return self.Count 

```



### Print All Subsequences Containing a Given Character

Use the If condition in the Function call to check the char is present or not , Instead of printing... 

```python 
a = input("Enter the String : ")
b = input("Enter the Char to Check : ")
RES = []
def REC(idx , lists):
    if idx == len(a):
        if b  in lists:
            RES.append(lists)
            # return True 
        # else:
            # return False 
        return 
    REC(idx + 1 , lists) 
        # return True 
    REC(idx + 1 , lists+[a[idx]]) 
        # return True 
    # return False 
Arr = []
Res =  REC(0,Arr)
if not RES :
    print("No char found")
else :
    print(RES)
```



### *[334. Increasing Triplet Subsequence](https://leetcode.com/problems/increasing-triplet-subsequence/)*



*Brute Force :* 

```python 
class Solution:
    def increasingTriplet(self, nums: List[int]) -> bool:
        for i in range(len(nums)):
            for j in range(i , len(nums)):
                for k in range(j, len(nums)):
                    if nums[i]<nums[j]<nums[k]:
                        return True 
        return False 

```

*Optimized One :* 

```python 
class Solution:
    def increasingTriplet(self, nums: List[int]) -> bool:
        First = math.inf
        Second = math.inf
                     # or  first, second = inf, inf
        for i in range(len(nums)):
            if nums[i] <= First:
                First = nums[i]
            elif nums[i] <= Second :
                Second = nums[i]
            else :
                return True
        return False 
```

