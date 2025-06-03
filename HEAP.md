

## 💡 What is a **Heap**?

A **heap** is a **special tree-based data structure** that satisfies the **heap property**.

There are two main types:

### ✅ 1. **Min-Heap**:

- Every parent node is **less than or equal to** its children.
    
- So, the **smallest** element is always at the root.
    

### ✅ 2. **Max-Heap**:

- Every parent node is **greater than or equal to** its children.
    
- So, the **largest** element is always at the root.


## ⏱️ Time Complexities

| Operation     | Time Complexity |
| ------------- | --------------- |
| Insert        | O(log n)        |
| Delete (Root) | O(log n)        |
| Peek (Root)   | O(1)            |
| Build Heap    | O(n)            |


## 📦 Why Do We Use a Heap?

Because it's **efficient** when you want to:

- Continuously access the **highest** or **lowest** priority item (like in a **priority queue**).
    
- Sort elements efficiently (Heap Sort).

Solve problems like:

- K largest/smallest elements
    
- Median of data stream
    
- Merging k sorted arrays/lists
    
- Scheduling (like OS or event management)


## 🧠 Heap Properties

1. **Complete Binary Tree**:
    
    - All levels are full except possibly the last, which is filled **from left to right**.
        
2. **Heap Property**:
    
    - For **min-heap**: `parent <= children`
        
    - For **max-heap**: `parent >= children`
        
3. **Efficient Implementation**:
    
    - Usually implemented as an **array**, not using tree nodes.
        
    - You don’t need pointers to children.
        
    
    **Array Index Mapping** (0-based):
    
    - Parent: `i`
        
    - Left child: `2i + 1`
        
    - Right child: `2i + 2`
        
    - Parent of node at `i`: `(i - 1) // 2`


# Why do we need to use the heap?

##  ✅ 1. **To Always Access the Highest or Lowest Priority Item Quickly**

### Why Heap?

- **Heap** keeps the **max or min element at the top**, always.
    
- You get:
    
    - **Peek (min/max)**: O(1)
        
    - **Insert**: O(log n)
        
    - **Remove min/max**: O(log n)
        

### Where It’s Useful:

- **Priority queues**
    
- **Task schedulers**
    
- __AI (A_ algorithm)_*
    
- **Dijkstra’s shortest path**
    

---

## ✅ 2. **To Handle Streaming or Dynamic Data**

### Why Heap?

- Merge sort, quick sort need **all data up front**.
    
- But what if:
    
    - Data is **arriving in chunks**?
        
    - You need to track the **top K elements** on the fly?
        

➡️ **Heap is ideal** for real-time updating and querying.

### Examples:

- **Kth largest element in a stream**
    
- **Median in a data stream** (using two heaps)
    

---

## ✅ 3. **To Solve Top-K or Partial Sorting Problems Efficiently**

### Why Heap?

- You don’t need to sort the **whole array**.
    
- You can just maintain a **heap of size k**.
    

### Examples:

- **Top K frequent words**
    
- **Top K largest numbers**
    
- **Sort a nearly sorted (k-sorted) array**
    

Using a heap is **faster and more memory-efficient** than full sorting in these cases.

---

## ✅ 4. **To Merge Multiple Sorted Lists**

### Why Heap?

- Keep track of the **smallest element from each list** in a min-heap.
    
- Pop the smallest, push the next from that list.
    

### Example:

- **Merge k sorted arrays/lists** in O(n log k)
    

No other structure makes this as efficient.

---

## ✅ 5. **To Implement a Priority Queue**

This is the most important practical use of a heap.

### Why Heap?

- It’s **designed** for this.
    
- No need for full sorting.
    
- Better than:
    
    - Array (slow to find min/max)
        
    - Linked list (slow insertion/removal)
        

Languages like Python (`heapq`), Java (`PriorityQueue`), and C++ (`priority_queue`) all use **heaps internally**.



## 📚 Topics to Learn in Heaps (Interview-Focused)

1. **Basics of Heap**
    
    - Min-Heap vs Max-Heap
        
    - Array implementation
        
2. **Heap Operations**
    
    - Insert
        
    - Delete
        
    - Heapify
        
    - Build Heap from Array
        
3. **Heap Sort**
    
4. **Priority Queue**
    
    - Implemented with heap
        
    - Use cases in real-world and algorithms
        
5. **Advanced Problems Using Heap**
    
    - K largest/smallest elements
        
    - Merge K sorted lists
        
    - Top K frequent elements
        
    - Median of a stream
        
    - Task scheduling
        
6. **Types of Heaps**
    
    - Binary Heap (most common)
        
    - Fibonacci Heap (used in advanced graph algorithms)
        
    - Binomial Heap (less common)
        
7. **Language-Specific Heap Tools**
    
    - Python: `heapq` (Min-Heap)
        
    - Java: `PriorityQueue`
        
    - C++: `priority_queue`




### 💡 Priority Queue vs. Heap

- **Priority Queue** is a **concept** (or abstract data type).
    
- **Heap** is a **data structure** commonly used to **implement** a priority queue.

### 📘 Analogy:

- A **car** (priority queue) takes you from A to B.
    
- The **engine** (heap) powers the car.



### INBUILD FUNCTION :  

Yes! ✅ Python provides a built-in **heap module** called `heapq` — it's part of the standard library and supports **Min Heap** functionality out of the box.

---

## ✅ `heapq` Module in Python

### 🔹 What it supports:

- Min Heap only (by default)
    
- Efficient `O(log n)` operations
    
- Works directly on **lists**
    

---

## 🔧 Basic Min Heap Example (Built-in)


```python
import heapq

# Initialize an empty heap
heap = []

# Push values
heapq.heappush(heap, 5)
heapq.heappush(heap, 1)
heapq.heappush(heap, 3)

# Peek at smallest (min)
print(heap[0])  # Output: 1

# Pop the smallest
print(heapq.heappop(heap))  # Output: 1
print(heapq.heappop(heap))  # Output: 3

```


---

## 🔄 Max Heap in Python (Using `heapq`)

Python's `heapq` only supports Min Heap — but we can simulate a **Max Heap** by inserting negative values:



```python 
import heapq

nums = [1, 5, 3, 10]
max_heap = []

# Push negatives
for num in nums:
    heapq.heappush(max_heap, -num)

# Pop max (i.e., smallest negative)
print(-heapq.heappop(max_heap))  # Output: 10

```




---

## 🧠 Summary of Built-in Heap Functions

|Function|Purpose|
|---|---|
|`heapq.heappush(heap, x)`|Pushes `x` into heap|
|`heapq.heappop(heap)`|Pops and returns smallest item|
|`heapq.heapify(list)`|Converts list into a heap|
|`heapq.heappushpop(heap, x)`|Pushes then pops in one step|
|`heapq.nlargest(k, iterable)`|Returns k largest elements|
|`heapq.nsmallest(k, iterable)`|Returns k smallest elements|
