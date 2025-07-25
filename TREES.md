Template for the BFS : 


Template for the BFS : In Simple Manner...  Or For the Simple Traversal Also...


```python 

class Solution :
	def Tree (self, Root): 
		if not Root : return [] or ""
		Queue = dequeue([Root])
		while Queue : 
			Node  = Queue.popleft()
			print(Node.val)
			if Node.left : 
				Queue.append(Node.left)
			if Node.right : 
				Queue.append(Node.right)
		
		
```

```python 

if root == None :

            return []

        res = []

        dd = deque([root])

        idx = 0

        while dd :

            sub = []

            for i in range(len(dd)):

                dk = dd.popleft()

                sub.append(dk.val)

                if dk.left :

                    dd.append(dk.left)

                if dk.right:

                    dd.append(dk.right)

            #if idx % 2  ==1 :

             #   res.append(list(reversed(sub)))

            #else :

            res.append(sub)

            idx = idx +1

        return res
```

-------------------------------------------------------------------------
### [104. Maximum Depth of Binary Tree](https://leetcode.com/problems/maximum-depth-of-binary-tree/)


```python 
# Definition for a binary tree node.

# class TreeNode:

#     def __init__(self, val=0, left=None, right=None):

#         self.val = val

#         self.left = left

#         self.right = right

class Solution:

    def maxDepth(self, root: Optional[TreeNode]) -> int:

        if root == None :

            return  0

        left = self.maxDepth (root.left)

        right = self.maxDepth(root.right)

        return max(left,right)+1
```

Using the BFS  : 

```python 

# Definition for a binary tree node.

# class TreeNode:

#     def __init__(self, val=0, left=None, right=None):

#         self.val = val

#         self.left = left

#         self.right = right

class Solution:

    def maxDepth(self, root: Optional[TreeNode]) -> int:

        if not root :

            return 0

        temp = root

        res = []

        stack = deque([root])

        while stack :

            sub = []

            for i in range(len(stack)):

                node = stack.popleft()

                sub.append(node.val)

                if node.left :

                    stack.append(node.left)

                if node.right:

                    stack.append(node.right)

            res.append(sub)

        print(res)

        return len(res)
```

### [100. Same Tree](https://leetcode.com/problems/same-tree/)

```python 
# Definition for a binary tree node.

# class TreeNode:

#     def __init__(self, val=0, left=None, right=None):

#         self.val = val

#         self.left = left

#         self.right = right

class Solution:

    def isSameTree(self, p: Optional[TreeNode], q: Optional[TreeNode]) -> bool:

        if not p and not q :

            return True

        if  not p or not q or p.val != q.val:

            return False

        return self.isSameTree(p.left,q.left)and self.isSameTree(p.right,q.right)
```

Using the BFS :


```python 
# Definition for a binary tree node.

# class TreeNode:

#     def __init__(self, val=0, left=None, right=None):

#         self.val = val

#         self.left = left

#         self.right = right

class Solution:

    def isSameTree(self, p: Optional[TreeNode], q: Optional[TreeNode]) -> bool:

        if not  p and not q :

            return True

        if not p or not q :

            return False

        if p.val != q.val :

            return False

        res = []

        stack = deque([p.left,q.left,p.right,q.right])

        while stack :

            node = stack.popleft()

            node1 = stack.popleft()

            if not node and not node1 :

                continue

            if not node or not node1:

                return False

            if node.val != node1.val :

                return False

            stack.append(node.left)

            stack.append(node1.left)

            stack.append(node.right)

            stack.append(node1.right)

        return True
```
### [144. Binary Tree Preorder Traversal](https://leetcode.com/problems/binary-tree-preorder-traversal/)

```python 
# Definition for a binary tree node.

# class TreeNode:

#     def __init__(self, val=0, left=None, right=None):

#         self.val = val

#         self.left = left

#         self.right = right

class Solution:

    def __init__(self):

        self.arr= []

    def preorderTraversal(self, root: Optional[TreeNode]) -> List[int]:

        if root == None :

            return self.arr

        self.arr.append(root.val)

        self.preorderTraversal(root.left)

        self.preorderTraversal(root.right)

        return self.arr


```


Using the iterative  Solution : 

```python 
# Definition for a binary tree node.

# class TreeNode:

#     def __init__(self, val=0, left=None, right=None):

#         self.val = val

#         self.left = left

#         self.right = right

class Solution:

    def preorderTraversal(self, root: Optional[TreeNode]) -> List[int]:

        res = []

        if not root :

            return []

        stack = [root]

        temp = root

        # since it is a pre order so root , left , right

        while stack :

            node = stack.pop()

            res.append(node.val)

            # since we first take the right first and then only we go to the left

            # this is due the LIFO of the stack behaviour

            if node.right:

                stack.append(node.right)

            if node.left :

                stack.append(node.left)

        return res
```

### [94. Binary Tree Inorder Traversal](https://leetcode.com/problems/binary-tree-inorder-traversal/)

```python 
# Definition for a binary tree node.

# class TreeNode:

#     def __init__(self, val=0, left=None, right=None):

#         self.val = val

#         self.left = left

#         self.right = right

class Solution:

    def __init__(self):

        self.arr=[]

    def inorderTraversal(self, root: Optional[TreeNode]) -> List[int]:

        if root == None :

            return self.arr

        self.inorderTraversal(root.left)

        self.arr.append(root.val)

        self.inorderTraversal(root.right)

        return self.arr
```
![[Pasted image 20250314162512.png]]
```python 
# Definition for a binary tree node.

# class TreeNode:

#     def __init__(self, val=0, left=None, right=None):

#         self.val = val

#         self.left = left

#         self.right = right

class Solution:

    def inorderTraversal(self, root: Optional[TreeNode]) -> List[int]:

        if root == None :

            return []

        return  self.inorderTraversal(root.left) + [root.val] + self.inorderTraversal(root.right)


```

Using the Iterative Solution : 
Hint :  
✔ **Go left until you can't**  
✔ **Pop the last node and process it**  
✔ **Move to the right subtree**

```python 
# Definition for a binary tree node.

# class TreeNode:

#     def __init__(self, val=0, left=None, right=None):

#         self.val = val

#         self.left = left

#         self.right = right

class Solution:

    def inorderTraversal(self, root: Optional[TreeNode]) -> List[int]:

        stack = []

        res = []

        temp = root

        while stack or temp :

            if temp:

                stack.append(temp)

                temp = temp.left

            else :

                node = stack.pop()  # After that it is taking the stack elements as a node and set as a right node and traversing to the right nodes 

                res.append(node.val)

                temp = node.right

        return res
```
### [145. Binary Tree Postorder Traversal](https://leetcode.com/problems/binary-tree-postorder-traversal/)

```python 
# Definition for a binary tree node.

# class TreeNode:

#     def __init__(self, val=0, left=None, right=None):

#         self.val = val

#         self.left = left

#         self.right = right

class Solution:

    def __init__(self):

        self.arr=[]

    def postorderTraversal(self, root: Optional[TreeNode]) -> List[int]:

        if root == None :

            return self.arr

        self.postorderTraversal(root.left)

        self.postorderTraversal(root.right)

        self.arr.append(root.val)

        return self.arr
```


Using the 2 stack : 

```python 

# Definition for a binary tree node.

# class TreeNode:

#     def __init__(self, val=0, left=None, right=None):

#         self.val = val

#         self.left = left

#         self.right = right

class Solution:

    def postorderTraversal(self, root: Optional[TreeNode]) -> List[int]:

        res  = []

        if not root :

            return []

        stack = []

        stack1 = [root]

        while stack1 :

            node = stack1.pop()

            stack.append(node.val)

            if node.left :

                stack1.append(node.left)

            if node.right :

                stack1.append(node.right)

        print(stack)

        while stack:

            res.append(stack.pop())

        return res
```


Using the single stack : 

```python 
# Definition for a binary tree node.

# class TreeNode:

#     def __init__(self, val=0, left=None, right=None):

#         self.val = val

#         self.left = left

#         self.right = right

class Solution:

    def postorderTraversal(self, root: Optional[TreeNode]) -> List[int]:

        if not root :

            return []

        stack = []

        stack1 = [root]

        while stack1 :

            node = stack1.pop()

            stack.append(node.val)

            if node.left :

                stack1.append(node.left)

            if node.right :

                stack1.append(node.right)

        return stack[::-1]
```
### [102. Binary Tree Level Order Traversal](https://leetcode.com/problems/binary-tree-level-order-traversal/)

BFS : 

```python 
# Definition for a binary tree node.

# class TreeNode:

#     def __init__(self, val=0, left=None, right=None):

#         self.val = val

#         self.left = left

#         self.right = right

class Solution:

    def levelOrder(self, root: Optional[TreeNode]) -> List[List[int]]:

        if not root :

            return []

        height = collections.deque([root])  # 2  Faster when compared to the Stack

        temp = root

        res = []

        while height :

            sub = []

            Len= len(height)

            for _ in range(Len):

                node = height.popleft() ## FIFO property #1

                sub.append(node.val)

                if node.left:

                    height.append(node.left)

                if node.right:

                    height.append(node.right)

            res.append(sub) #3

        return res
```

### [222. Count Complete Tree Nodes](https://leetcode.com/problems/count-complete-tree-nodes/)

Using the BFS

```python 
# Definition for a binary tree node.

# class TreeNode:

#     def __init__(self, val=0, left=None, right=None):

#         self.val = val

#         self.left = left

#         self.right = right

class Solution:

    def countNodes(self, root: Optional[TreeNode]) -> int:

        if not root  :

            return 0

        res = []

        count = 0

        stack = deque([root])

        while stack :

            sub  = []

            for i in range(len(stack)):

                node = stack.popleft()

                count  = count + 1

                sub.append(node.val)

                if node.left:

                    stack.append(node.left)

                if node.right:

                    stack.append(node.right)

            res.append(sub)

        return count
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


### [617. Merge Two Binary Trees](https://leetcode.com/problems/merge-two-binary-trees/)


```python 
# Definition for a binary tree node.

# class TreeNode:

#     def __init__(self, val=0, left=None, right=None):

#         self.val = val

#         self.left = left

#         self.right = right

class Solution:

    def mergeTrees(self, root1: Optional[TreeNode], root2: Optional[TreeNode]) -> Optional[TreeNode]:

        if root1 == None :

            return root2

        if root2 == None :

            return root1

        root1.val += root2.val

        root1.left = self.mergeTrees(root1.left,root2.left)

        root1.right = self.mergeTrees(root1.right,root2.right)

        return root1
```



### Ceil in BST

```python 

class Solution:
    def findCeil(self,root, x):
        # code here
        temp = -1  

        while root:
            if root.key == x:  
                return root.key
            elif root.key > x:
                temp = root.key  
                root = root.left  
            else:
                root = root.right  
        return temp 
           
```

BFS : 

Here  we are only checking the ceil of the element , if Not keep a var and track the element 

```python 
''' class Node:
    def __init__(self, val):
        self.right = None
        self.key = val
        self.left = None '''
import math   
class Solution:
    def findCeil(self,root, X):
        # code here
        if not root :
            return None 
        Stack = deque([root])
        Min = math.inf  #### IMPORTANT 
        while Stack :
            Node = Stack.popleft()
            if math.ceil( Node.key ) == X :
                return Node.key  
            elif Node.key > X: ##### IMPORTANT 
                # Candidate for ceil
                Min = min(Min, Node.key) ######## IMPORTANT
            if Node.left :
                Stack.append(Node.left)
            if Node.right:
                Stack.append(Node.right)
        # return None
        return Min if Min !=  math.inf else -1 
                
            
```

### Floor in BST

```python 

class Solution:
    def floor(self, root, x):
        # Code here
        floor_val = -1 
        while root :
            if root.data == x :
                return root.data
            elif (root.data> x):
                root = root.left
            else :
                floor_val  = root.data
                root= root.right
        return floor_val 
```


### Array to BST

```python 
class Solution:
    def sortedArrayToBST(self, arr):
        # code here
        def recur(nums,start,end):
            if start > end :
                return None 
            mid = start+(end-start)//2
            root = Node(arr[mid])
            
            root.left = recur(arr,start,mid-1)
            root.right = recur(arr,mid+1,end)
            return root
        return recur(arr,0 , len(arr)-1)
```



### BFS : 

### [107. Binary Tree Level Order Traversal II](https://leetcode.com/problems/binary-tree-level-order-traversal-ii/) 


```python 
# Definition for a binary tree node.

# class TreeNode:

#     def __init__(self, val=0, left=None, right=None):

#         self.val = val

#         self.left = left

#         self.right = right

class Solution:

    def levelOrderBottom(self, root: Optional[TreeNode]) -> List[List[int]]:

        def BFS (root):

            res = []

            if not root :

                return []

            stack  = deque ([root])

            while stack :

                sub = []

                for i in range(len(stack)):

                    node = stack.popleft()

                    sub.append(node.val)

                    if node.left :

                        stack.append(node.left)

                    if node.right:

                        stack.append(node.right)

                res.append(sub)

            return res

        return list(reversed(BFS(root))) # use the list for unpacking the ojects
```


### [111. Minimum Depth of Binary Tree](https://leetcode.com/problems/minimum-depth-of-binary-tree/)

```python 
# Definition for a binary tree node.

# class TreeNode:

#     def __init__(self, val=0, left=None, right=None):

#         self.val = val

#         self.left = left

#         self.right = right

class Solution:

    def minDepth(self, root: Optional[TreeNode]) -> int:

        stack  = deque ([root])

        idx = 0

        while stack :

            for i in range(len(stack)):

                node = stack.popleft()

                if not node.right and not node.left : # in the question A leaf node without no childern # core part of the question 

                    return  idx + 1

                if node.left :

                    stack.append(node.left)

                if node.right:

                    stack.append(node.right)

            idx += 1

        return idx
```

### [199. Binary Tree Right Side View](https://leetcode.com/problems/binary-tree-right-side-view/)

```python 
# Definition for a binary tree node.

# class TreeNode:

#     def __init__(self, val=0, left=None, right=None):

#         self.val = val

#         self.left = left

#         self.right = right

class Solution:

    def rightSideView(self, root: Optional[TreeNode]) -> List[int]:

        if not root :

            return []

        def BFS (root):

            if not root :

                return []

            res = []

            stack = deque([root])

            while stack :

                sub = []

                for i in range(len(stack)):

                    node   = stack.popleft()

                    sub.append(node.val)

                    if node.left:

                        stack.append(node.left)

                    if node.right:

                        stack.append(node.right)

                res.append(sub)

            return res

        dd = list(BFS(root))

        dk = []

        for i in range(len(dd)):

            dk.append((dd[i][-1]))

        return dk
```

### [637. Average of Levels in Binary Tree](https://leetcode.com/problems/average-of-levels-in-binary-tree/)


```python 
# Definition for a binary tree node.

# class TreeNode:

#     def __init__(self, val=0, left=None, right=None):

#         self.val = val

#         self.left = left

#         self.right = right

class Solution:

    def averageOfLevels(self, root: Optional[TreeNode]) -> List[float]:

        if not root :

            return 0

        def BFS (root)->list:

            if not root :

                return 0

            stack  = deque([root])

            res = []

            while stack :

                # sub = []

                Sum = 0

                Count = 0

                for i in range(len(stack)):

                    node = stack.popleft()

                    Sum = Sum + node.val

                    Count += 1

                    if node.left :

                        stack.append(node.left)

                    if node.right:

                        stack.append(node.right)

                res.append(Sum/Count)

            print(res)

            return res

        return BFS(root)
```


### [116. Populating Next Right Pointers in Each Node](https://leetcode.com/problems/populating-next-right-pointers-in-each-node/)


```python 
"""

# Definition for a Node.

class Node:

    def __init__(self, val: int = 0, left: 'Node' = None, right: 'Node' = None, next: 'Node' = None):

        self.val = val

        self.left = left

        self.right = right

        self.next = next

"""

  

class Solution:

    def connect(self, root: 'Optional[Node]') -> 'Optional[Node]':

        def BFS(root):

            if not root :

                return None

            res = []

            stack = deque([root])

            while stack:
	            # Level = len(stack)-1
				 #Populate the next pointer
                for i in range(len(stack)-1):

                    stack[i].next = stack[i+1]
                 # Iterate through q -- Add all children

                for i in range(len(stack)):

                    node = stack.popleft()

                    # if Level -1 > i :

                    #     node.next = stack[0]

                    if node.left :

                        stack.append(node.left)

                    if node.right:

                        stack.append(node.right)

            return root

        return BFS(root)
```

or 
```python 
  

class Solution:

    def connect(self, root: 'Optional[Node]') -> 'Optional[Node]':

        if not root :

            return None

        def BFS(root):

            if not root:

                return None

            res = []  

            stack = deque([root])

            while stack:

                sub = []

                for i in range(len(stack)):

                    node = stack.popleft()

                    sub.append(node)

                    if node.left:

                        stack.append(node.left)

                    if node.right:

                        stack.append(node.right)

                for i in range(len(sub)-1):

                    sub[i].next = sub[i+1]

            return root

        return BFS(root)
```
### [117. Populating Next Right Pointers in Each Node II](https://leetcode.com/problems/populating-next-right-pointers-in-each-node-ii/) 

```python 
class Solution:

    def connect(self, root: "Optional[Node]") -> "Optional[Node]":

        if not root:

            return None

  

        def BFS(root):

            if not root:

                return None

            res = []

            stack = deque([root])

            while stack:

                level = len(stack) - 1

                for i in range(len(stack)):

                    node = stack.popleft()

                    if node.left:

                        stack.append(node.left)

                    if node.right:

                        stack.append(node.right)

                    if level > i:

                        node.next = stack[0]

            return root

  

        return BFS(root)
```


### Bottom View of Binary Tree

```python 
class Solution:
    def bottomView(self, root):
        if not root :
            return  0 
        def BFS(root):
            if not root :
                return 0 
            dd = {}
            stack = deque([ (root,0) ]) #### 
            while stack :
                for i in range(len(stack)):
                    node , col = stack.popleft()
                    if col not in dd :
                        dd[col] = node.data
                    else :
                        dd[col] = node.data
                    if node.left:
                        stack.append((node.left, col -1))
                    if node.right:
                        stack.append((node.right , col +1 )) # append single arg 
            # print(dd)
            return dd 
        dk = BFS(root)
        return [dk[i] for i in sorted(dk.keys())]
```


### Top View of Binary Tree

```python 

# Tree Node
# class Node:
#     def __init__(self, val):
#         self.right = None
#         self.data = val
#         self.left = None

class Solution:
    def topView(self,root):
        # code here
        def BFS (root):
            if not root :
                return 0 
            stack = deque([(root, 0)])
            dd ={}
            while stack :
                for i in range(len(stack)):
                    node, col = stack.popleft()
                    if col not in dd :
                        dd[col] = node.data
                    if node.left :
                        stack.append((node.left, col -1 ))
                    if node.right:
                        stack.append((node.right,col +1 ))
            # print(dd)
            return dd 
        dk = BFS(root)
        return [dk[i] for i in sorted(dk.keys())]
```


### Left View of Binary Tree 

```python 
class Solution:
    
    def LeftView(self, root):
        def BFS(root):
            if not root :
                return []
            res = []
            stack  = deque([root])
            while stack :
                sub = []
                for i in range(len(stack)):
                    node = stack.popleft()
                    sub.append(node.data)
                    if node.left:
                        stack.append(node.left)
                    if node.right:
                        stack.append(node.right)
                res.append(sub)
            return res
        dd = BFS(root)
        return [dd[i][0] for i in range(len(dd))]
```



### [101. Symmetric Tree](https://leetcode.com/problems/symmetric-tree/)

```python 
# Definition for a binary tree node.

# class TreeNode:

#     def __init__(self, val=0, left=None, right=None):

#         self.val = val

#         self.left = left

#         self.right = right

class Solution:

    def isSymmetric(self, root: Optional[TreeNode]) -> bool:

        if not root :

            return False

        def BFS (root):

            if not root :

                return []

            stack = deque([(root.left, root.right)]) # Important Next to the root conditions

            res =[]

            while stack :

                for i in range(len(stack)):

                    node_left, node_right = stack.popleft()

                    if not node_left and not node_right:

                        continue  # Both are None, symmetry holds

                    if not node_left or   not node_right or node_left.val != node_right.val :

                        return False #asymetric found 

                     # Push child nodes in mirrored order
	                stack.append((node_left.left, node_right.right))
	                stack.append((node_left.right, node_right.left)) 

            return True

        return BFS(root)
```




### Tree Boundary Traversal


```python 

'''
class Node:
    def __init__(self, val):
        self.right = None
        self.data = val
        self.left = None
'''


class Solution:
    def boundaryTraversal(self, root):
        # Code here
        if root is None:
            return []
        result = []
        
        def left(root):
            curr = root.left
            while curr:
                if curr.left is None and curr.right is None:
                    break
                result.append(curr.data)
                
                if curr.left:
                    curr = curr.left
                else:
                    curr = curr.right
                    
        def right(root):
            stack = []
            curr = root.right
            while curr:
                if curr.left is None and curr.right is None:
                    break    
                stack.append(curr.data)

                if curr.right:
                    curr = curr.right
                else:
                    curr = curr.left
            #  reverse the elements       
            while stack:
                value = stack.pop()
                result.append(value)
        #   Inorder      
        def leaf_nodes(root):
            
            if root is None:
                return
            
            if root.left is None and root.right is None:
                result.append(root.data)
                return
            
            if root.left:
                leaf_nodes(root.left)
            if root.right:
                leaf_nodes(root.right)
                
        if root.left or root.right:
            result.append(root.data)

        left(root)
        leaf_nodes(root)
        right(root)
        
        return result
```


### [230. Kth Smallest Element in a BST](https://leetcode.com/problems/kth-smallest-element-in-a-bst/)

Using the BFS  : 


```python 
# Definition for a binary tree node.

# class TreeNode:

#     def __init__(self, val=0, left=None, right=None):

#         self.val = val

#         self.left = left

#         self.right = right

class Solution:

    def kthSmallest(self, root: Optional[TreeNode], k: int) -> int:

        def BFS (root):

            if not root :

                return []

            dd = []

            stack  = deque([root])

            while stack :

                for i in range(len(stack)):

                    Node = stack.popleft()

                    dd.append(Node.val)

                    if Node.left :

                        stack.append(Node.left)

                    if Node.right:

                        stack.append(Node.right)

            print(dd)

            return dd

        dk = sorted(BFS(root))

  

        return dk[k-1]
```


Using the DFS  : 

 It is not optimized , Stop the code when the k th element is found . Naturally it is in a sorted order only. Use the Normal inorder using the stack and in the iterative Approach.
  
```python 
# Definition for a binary tree node.

# class TreeNode:

#     def __init__(self, val=0, left=None, right=None):

#         self.val = val

#         self.left = left

#         self.right = right

class Solution:

    def kthSmallest(self, root: Optional[TreeNode], k: int) -> int:

        def inorder(root):

            if root  == None :

                return []

            return inorder(root.left) + [root.val] + inorder(root.right)

        dk = inorder(root)

        return (dk[k-1])
```

Optimized  : 
✅ **Uses early exit (`O(k) time`)**

```python 
# Definition for a binary tree node.

# class TreeNode:

#     def __init__(self, val=0, left=None, right=None):

#         self.val = val

#         self.left = left

#         self.right = right

class Solution:

    def kthSmallest(self, root: Optional[TreeNode], k: int) -> int:

        if root is None :

            return None

        def inorder(root):

            if root is None :

                return []

            # res = []

            temp = root

            stack = []

            count = 0

            while stack or temp:

                if temp :

                    stack.append(temp)

                    temp = temp.left

                else :

                    Node = stack.pop()

                    count +=1

                    if count == k :

                        return Node.val

                    # res.append(Node.val)

                    temp = Node.right # Not the Temp.right

            # print(res)

            return None

        return inorder(root)
```


###  [965. Univalued Binary Tree](https://leetcode.com/problems/univalued-binary-tree/)


```python 
class Solution:
    def isUnivalTree(self, root: Optional[TreeNode]) -> bool:
        if not root : return False 
        Target = root.val
        Queue = deque([root])
        while Queue :
            Node = Queue.popleft()
            if Node.val != Target : return False 
            if Node.left :
                Queue.append(Node.left)
            if Node.right :
                Queue.append(Node.right)
        return True
```

----


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