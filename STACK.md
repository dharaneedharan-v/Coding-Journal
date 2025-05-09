### Implement stack using array

```python 
class MyStack:
    
    def __init__(self):
        self.arr=[] * 1000
        
    def push(self,data):
        return self.arr.append(data)
    def pop(self):
        if not self.arr:
            return -1 
        return self.arr.pop()
```
 Static Sized Array Implementation:   
```python 
class MyStack:
    
    def __init__(self):
        self.arr=[0]*100
        self.size = 0
    
    #Function to push an integer into the stack.
    def push(self,data):
        #add code here
        self.arr[self.size]=data
        self.size+=1
    
    #Function to remove an item from top of the stack.
    def pop(self):
        #add code here
        if self.size<=0:
            return -1
        self.size-=1
        return self.arr[self.size]
```



### Implement Queue Using Array

 Same code for the stack Just  a Small change in the Pop operation , In Queue , It is popped form the Left Not the Right  Use the Pop(0) 
 
```python 
class MyQueue:
    
    #Function to push an element x in a queue.
    def __init__(self):
        self.arr = [] * 1000
        
    def push(self, x):
        return self.arr.append(x)
     
    def pop(self): 
        if not self.arr:return -1
        return  self.arr.pop(0) 
```

Static Sized Array Implementation : 

 + Just Assign the X value to it 
 +  Make it a Circular Queue   
 + For that take the modulo [ REAR OR FRONT % SIZE ]  
 
```python 
class MyQueue: 
	def __init__(self):
        self.capacity = 100000
        self.queue = [None] * self.capacity  # Static array
        self.front = 0
        self.rear = 0
        self.size = 0

    def push(self, x):
        if self.size == self.capacity:
            print("Queue is full")
            return  0
        self.queue[self.rear] = x  # Assign it 
        self.rear = (self.rear + 1) % self.capacity
        self.size += 1


    def pop(self):
        if self.size == 0:
            return -1
        x = self.queue[self.front] # Assign it
        self.front = (self.front + 1) % self.capacity
        self.size -= 1
        return x
```





===============================================================
### [20. Valid Parentheses](https://leetcode.com/problems/valid-parentheses/)

APPROACH  :
 - **Push corresponding closing brackets** onto the stack when encountering an opening bracket (`(` → `)`, `{` → `}`, `[` → `]`).
- **Pop and check** when encountering a closing bracket:
    - If the stack is empty (no matching opening bracket), return `False`.
    - If the popped bracket does not match the current closing bracket, return `False`.
- **At the end**, return `True` **only if the stack is empty** (all brackets matched correctly).
```PYTHON 
class Solution:

    def isValid(self, s: str) -> bool:

        dd = []

        if len(s) == 1 :

            return False

        for i in s :

            if i == "(":

                dd.append(")")

            elif i == "{":

                dd.append("}")

            elif i == "[":

                dd.append("]")

            else :
				#Check the stack is empty or not 
                if not dd :

                    return False

                k = dd.pop()

                if k != i :

                    return False
#return True only the len of the stack is 0 
        return len(dd) == 0  # The core part of the code is here only if the stack is not empty means return False of the similar brackets alone there. =============IMPORTANT===================
```


### Monotonic Stack : 

### [402. Remove K Digits](https://leetcode.com/problems/remove-k-digits/)

```python 
class Solution:
    def removeKdigits(self, nums: str, k: int) -> str:
        stack = []
        for i in range(len(nums)) :
            while  stack and k > 0 and stack[-1] > nums[i]:
                stack.pop()
                k = k-1
            stack.append(nums[i])
        print(stack)
        if k > 0 :
            stack =  stack[:-k]
        return "".join(stack).lstrip("0") or "0"

```


