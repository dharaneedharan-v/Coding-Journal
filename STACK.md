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



# QUEUE : 

### METHODS : 


|Method|Description|
|---|---|
|`put(item)`|Adds `item` to the **back** of the queue.|
|`get()`|Removes and returns the **front** item from the queue.|
|`empty()`|Returns `True` if the queue is empty, else `False`.|
|`full()`|Returns `True` if the queue is full (if a `maxsize` was set).|
|`qsize()`|Returns the **approximate number** of items in the queue.|
|`put_nowait(item)`|Same as `put(item)`, but doesn't wait if the queue is full.|
|`get_nowait()`|Same as `get()`, but raises `queue.Empty` if the queue is empty.|


Example : 

```python 
from queue import Queue

# Create a new Queue
q = Queue()

# Add items to the queue
q.put(10)
q.put(20)
q.put(30)

# Check size
print("Queue size:", q.qsize())  # Output: 3

# Get the front item (removes it)
print("Dequeued item:", q.get())  # Output: 10

# Peek at the front item using internal list (not recommended in real code)
print("Peek (unsafe):", q.queue[0])  # Output: 20

# Check if the queue is empty
print("Is empty?", q.empty())  # Output: False

```

### Example of `get_nowait()`

```python 
from queue import Queue, Empty

# Create a queue and add two items
q = Queue()
q.put(100)
q.put(200)

try:
    print("Removed:", q.get_nowait())  # Output: 100
    print("Removed:", q.get_nowait())  # Output: 200

    # Try to remove one more item (queue is now empty)
    print("Removed:", q.get_nowait())

except Empty:
    print("Queue is empty! Nothing to remove.")

```


output : 

```python 
Removed: 100
Removed: 200
Queue is empty! Nothing to remove.

```

### Example with `put_nowait()`

```python 
from queue import Queue, Full

# Create a queue with maxsize 2
q = Queue(maxsize=2)

try:
    q.put_nowait(10)
    print("Added 10")

    q.put_nowait(20)
    print("Added 20")

    # Try to add a third item (should raise an exception)
    q.put_nowait(30)
    print("Added 30")

except Full:
    print("Queue is full! Couldn't add 30.")

```


output : 

```python 
Added 10
Added 20
Queue is full! Couldn't add 30.

```


### [225. Implement Stack using Queues](https://leetcode.com/problems/implement-stack-using-queues/)


```python 
from queue import Queue
class MyStack:

    def __init__(self):
        self.Queue = Queue()
        

    def push(self, x: int) -> None:
        self.Queue.put(x)
        for i in range(self.Queue.qsize()-1):
            self.Queue.put(self.Queue.get()) # First get the element and then put it in the Last. 
    def pop(self) -> int:
        return self.Queue.get()

    def top(self) -> int:
        return self.Queue.queue[0] # Inbulid Queue to take the Top Element 
        
    def empty(self) -> bool:
        return self.Queue.empty()


# Your MyStack object will be instantiated and called as such:
# obj = MyStack()
# obj.push(x)
# param_2 = obj.pop()
# param_3 = obj.top()
# param_4 = obj.empty()
```


### [232. Implement Queue using Stacks](https://leetcode.com/problems/implement-queue-using-stacks/)

I have Made the Pop and the Peek Operation Costly... 
TC  -> O(2 N)

```python 
class MyQueue:

    def __init__(self):
        self.s1 = []
        self.s2 = []

    def push(self, x: int) -> None:
        self.s1.append(x)
        
    def pop(self) -> int:
	        if not self.s2 : # if the S2 is empty [ True ]
            while self.s1 :
                self.s2.append(self.s1.pop())
        return self.s2.pop()

    def peek(self) -> int:
        if not self.s2 :
            while self.s1:
                self.s2.append(self.s1.pop())
        return self.s2[-1]

    def empty(self) -> bool:
        return not self.s1 and not self.s2 


# Your MyQueue object will be instantiated and called as such:
# obj = MyQueue()
# obj.push(x)
# param_2 = obj.pop()
# param_3 = obj.peek()
# param_4 = obj.empty()
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


