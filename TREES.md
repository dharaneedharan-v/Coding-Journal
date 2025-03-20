Template for the BFS : 

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


Using the iterative Solution : 

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