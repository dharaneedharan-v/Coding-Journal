### BINARY SEARCH TREE : 


## ✅ 1. What is a Binary Search Tree (BST)?

A **Binary Search Tree** is a type of binary tree where for every node:

- All nodes in the **left subtree** have values **less than** the node.
    
- All nodes in the **right subtree** have values **greater than** the node.
    

This structure allows **efficient searching, insertion, and deletion**.

---

## ✅ 2. Why do we use BSTs?

- They provide **logarithmic time complexity** (O(log n)) for:
    
    - Searching
        
    - Insertion
        
    - Deletion
        
- If the tree is **balanced**, these operations are **much faster** than linear structures like arrays or linked lists.
    

---

## ✅ 3. How does a BST work?

For example, if we insert values:  
`[8, 3, 10, 1, 6, 14]`

The BST looks like:

```
       8
      / \
     3   10
    / \    \
   1   6    14

```
- To **search** for a value (e.g., 6), we compare:
    
    - 6 < 8 → go left
        
    - 6 > 3 → go right
        
    - 6 == 6 → found!
        

This **binary decision at each node** is what gives BSTs their speed.

---

## ✅ 4. Real-time Use Cases

|Use Case|How BST Helps|
|---|---|
|Database indexing (e.g., B-Trees)|Organizes and searches large datasets fast|
|Auto-complete in search bars|Prefix trees and variants of BST|
|Routing tables in networks|Quick lookup of IP ranges|
|File system organization|Tree-based paths and indexing|
|Memory allocation in OS|BSTs help track available memory blocks|

---

## ✅ 5. Comparison With Other Data Structures

|Data Structure|Search|Insert|Delete|Sorted Access|Notes|
|---|---|---|---|---|---|
|**BST**|O(log n)|O(log n)|O(log n)|✅ Easy via in-order|Only if balanced|
|**Array**|O(n)|O(n)|O(n)|✅ (if sorted)|Fast indexing, slow insert/delete|
|**Linked List**|O(n)|O(1)|O(1)|❌|Sequential search only|
|**HashMap**|O(1)|O(1)|O(1)|❌|No ordering|
|**Heap**|O(n)|O(log n)|O(log n)|❌|Only min/max access|

So BSTs are best when you want:

- **Fast search**
    
- **Sorted traversal**
    
- **Dynamic inserts/deletes**
    

---

## ✅ 6. Purpose — Why Do We Need BST?

We need BSTs when:

- **Ordering** matters (e.g., range queries, sorted data)
    
- **Fast dynamic operations** (not just fixed-size lookup like arrays)
    
- **Balancing time vs. memory trade-offs** for real-world apps
    

---

## ✅ 7. How to Answer in an Interview (Example Response)

> **Q: Can you explain what a Binary Search Tree is and where it's useful?**

### 🎤 Sample Interview Answer:

> A **Binary Search Tree (BST)** is a binary tree where every node’s left child contains a value less than the node, and the right child contains a value greater than the node.
> 
> This structure allows us to **search, insert, and delete values in O(log n)** time if the tree is balanced.
> 
> It's used in situations where data needs to be kept **sorted** but still **dynamically updated**, such as:
> 
> - Implementing ordered maps/sets
>     
> - Databases (B-trees are generalized BSTs)
>     
> - Memory management in OS
>     
> 
> Compared to arrays, BSTs allow faster insert/delete. Compared to hash maps, BSTs provide **sorted order** and **range queries**.
> 
> For example, if I want to find all values between 10 and 30, it's very easy to do with an in-order traversal in BST.
> 
> In interview problems, I often use BSTs when:
> 
> - I need **logarithmic time performance**
>     
> - I need to **maintain order**
>     
> - Or when the question involves **"k-th smallest"**, **range checks**, or **dynamic datasets**
>     

---

## ✅ 8. Bonus: Tips in Interviews

- Mention **edge cases** (e.g., what if tree becomes unbalanced?)
    
- Talk about **balanced BSTs** like **AVL Trees** or **Red-Black Trees**
    
- If time, mention how **BSTs degrade to linked list (O(n))** if not balanced
    
- Use **in-order traversal** to show how BST gives **sorted order**
    

---

## ✅ In One Line:

> "A BST is a tree that keeps data sorted and allows efficient (O(log n)) search, insert, and delete — it’s the backbone of many ordered data structures in real-world systems like databases, memory managers, and file systems."


----
----


### Floor in BST:

```python 
#User function Template for python3
from collections import deque 
import math 
class Node:
    def __init__(self,val):
        self.right  = None 
        self.left = None 
        self.data =  val 
        
class Solution:
    def floor(self, root, x):
        # Code here
        Floor = -math.inf 
        Stack = deque([root])
        while Stack:
            Node = Stack.popleft()
            if Node.data == x :
                return Node.data 
            if Node.data < x :
                Floor = max(Floor , Node.data)
            if Node.left :
                Stack.append(Node.left)
            if Node.right :
                Stack.append(Node.right)
        return Floor if Floor != -math.inf else -1 
            
```

###  [701. Insert into a Binary Search Tree](https://leetcode.com/problems/insert-into-a-binary-search-tree/)

```python 
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right

class Solution:
    def insertIntoBST(self, root: Optional[TreeNode], x: int) -> Optional[TreeNode]:
        if root is None :
            return TreeNode(x)

        Stack = deque([root])
        while Stack :
            Node = Stack.popleft()
            if Node.val > x :
                if not Node.left :
                    Node.left = TreeNode(x)
                    return root 
                else :
                    Stack.append(Node.left)
            
            else :
                if not Node.right :
                    Node.right = TreeNode(x)
                    return root
                else :
                    Stack.append(Node.right)

```

### [230. Kth Smallest Element in a BST](https://leetcode.com/problems/kth-smallest-element-in-a-bst/)


```python 
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def kthSmallest(self, root: Optional[TreeNode], k: int) -> int:
        Stack = deque([root])
        Val = []
        while Stack:
            Node = Stack.popleft()
            Val.append(Node.val) 
            if Node.left:
                Stack.append(Node.left)
            if Node.right:
                Stack.append(Node.right)
        print(Val)
        dk = sorted(Val)
        print(dk)
        print(dk[k-1])
        return dk[k-1]
```

### [98. Validate Binary Search Tree](https://leetcode.com/problems/validate-binary-search-tree/)

```python 
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def isValidBST(self, root: Optional[TreeNode]) -> bool:
        Min , Max = -math.inf , math.inf ### IMPORTANT 
        Stack = deque([(root , Min , Max) ]) ### CORRECT INITIALIZATION OF TUPLES 
        while Stack :
            Node , Min , Max  = Stack.popleft()
            if not  (Min < Node.val < Max): #### IMPORTANT 
                return False 
            # print(Node , Min , Max )
            if Node.left :
                Stack.append((Node.left , Min , Node.val)) ###IMPORTANT 
            if Node.right :
                Stack.append((Node.right, Node.val , Max )) ###IMPORTANT 
        return True 
```


### [1008. Construct Binary Search Tree from Preorder Traversal](https://leetcode.com/problems/construct-binary-search-tree-from-preorder-traversal/)

```python 
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def bstFromPreorder(self, preorder: List[int]) -> Optional[TreeNode]:
        Tree = TreeNode(preorder[0])
        def BST_CONSTRUCT_REC(root , idx ):
            if root is None :
                return TreeNode(idx)
            if idx < root.val :
                root.left = BST_CONSTRUCT_REC(root.left , idx) ### IMPORTANT root.left in the recursive call
            else  :
                root.right = BST_CONSTRUCT_REC(root.right , idx)
            return root 
            
        for i in range(1,len(preorder)):
            BST_CONSTRUCT_REC(Tree , preorder[i])
        return Tree

```


###  Predecessor And Successor In BST


Not Optimal Approach , Interviewer Not  Statisify this with this code ..

```python 
from os import *
from sys import *
from collections import *
from math import *

'''
    ------- Binary Tree node structure -------
            class   BinaryTreeNode :
                def __init__(self, data) :
                    self.data = data
                    self.left = None
                    self.right = None

                def __del__(self):
                    if self.left:
                        del self.left
                    if self.right:
                        del self.right
      
'''

def predecessorSuccessor(root, key):

    Sort = []
    Stack = deque([root])
    while Stack :
        Node = Stack.popleft()
        Sort.append(Node.data)
        if Node.left :
            Stack.append(Node.left)
        if Node.right:
            Stack.append(Node.right)
    dk = sorted(Sort)
    # print(dk)
    Max = None 
    Min = None 

    for i in dk:
        if i < key :
            Min = i 
        elif i > key :
            Max = i
            break
    if Min==None :
        Min = -1 
    if  Max == None :
        Max =  -1 
    return Min,Max 
        
    # for i in range(len(dk)):
    #     if dk[i] == key:
    #         if i + 1 < len(dk):
    #             Max = dk[i + 1]
    #         if i - 1 >= 0:
    #             Min = dk[i - 1]
    #         break
    #     elif dk[i] > key:
    #         Max = dk[i]
    #         break
    #     else:
    #         Min = dk[i]

    # return Min if Min is not None else -1, Max if Max is not None else -1
            

```


### Merge two BST 's

Not Optimized One... 
Brute One : 

```python 
from collections import deque 
class Solution:
    def merge(self, root1, root2):
        # code here
        def Take_Elements(root):
            Stack = deque([root])
            Res = []
            while Stack :
                Node = Stack.popleft()
                Res.append(Node.data)
                if Node.left:
                    Stack.append(Node.left)
                if Node.right :
                    Stack.append(Node.right)
            return Res 

        dk = Take_Elements(root1)
        kd = Take_Elements(root2)
        Sorted = sorted(dk + kd) 
        return Sorted

        
```


### Pair Sum in BST

Not a optimized One... .

```python 
'''
# Tree Node
class Node:
    def __init__(self, val):
        self.right = None
        self.data = val
        self.left = None

'''
from collections import deque 

class Solution:
    def findTarget(self, root, Target): 
        # your code here.
        Res = []
        Stack = deque([root])
        while Stack :
            Node = Stack.popleft()
            Res.append(Node.data)
            if Node.left :
                Stack.append(Node.left)
            if Node.right :
                Stack.append(Node.right)
        # print(Res)
        # TLE : 
        # for i in range(len(Res)):
        #     for j in range(i+1 ,len(Res)):
        #         if Res[i] + Res[j] == Target :
        #             return True 
        # return False
        
        # Two pointer Concept : 
        Set  = set()
        
        for i in range(len(Res)):
            if Target- Res[i] in Set :
                return True 
            Set.add(Res[i])
        return False 
    
            
        
        
```


### [700. Search in a Binary Search Tree](https://leetcode.com/problems/search-in-a-binary-search-tree/)

Using the BFS: 
```python 
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def searchBST(self, root: Optional[TreeNode], val: int) -> Optional[TreeNode]:
        Stack = deque([root])
        while Stack :
            Node = Stack.popleft()
            if Node.val == val :
                return Node 
            if Node.left :
                Stack.append(Node.left)
            if Node.right :
                Stack.append(Node.right)
        return None 
```

Using the iterative method 
```python 
# Definition for a binary tree node.

# class TreeNode:

#     def __init__(self, val=0, left=None, right=None):

#         self.val = val

#         self.left = left

#         self.right = right

class Solution:

    def searchBST(self, root: Optional[TreeNode], val: int) -> Optional[TreeNode]:

        temp = root

        if root == None :

            return None

        while temp :

            if root.val == val :

                return root

            elif root.val > val :

                return self.searchBST(root.left,val)

            else :

                return self.searchBST(root.right, val)

        return temp
```

Using the Recursion : 

This is only the optimal , Logically The BST is a balanced Tree..  So go for the Binary Search Instead of the Linear Search... 

```python 
# Definition for a binary tree node.

# class TreeNode:

#     def __init__(self, val=0, left=None, right=None):

#         self.val = val

#         self.left = left

#         self.right = right

class Solution:

    def searchBST(self, root: Optional[TreeNode], val: int) -> Optional[TreeNode]:
		# check the root.val > val :left else:right side traversal , here return the root alone. 
        if not root:

            return None

        if root.val > val:

            return self.searchBST(root.left, val)

        if root.val < val:

            return self.searchBST(root.right, val)

        return root
```


