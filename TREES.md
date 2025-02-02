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

### [102. Binary Tree Level Order Traversal](https://leetcode.com/problems/binary-tree-level-order-traversal/)

Using the recursion 

```python 
# Definition for a binary tree node.

# class TreeNode:

#     def __init__(self, val=0, left=None, right=None):

#         self.val = val

#         self.left = left

#         self.right = right

class Solution:

    def levelOrder(self, root: Optional[TreeNode]) -> List[List[int]]:

        res = []

        if root == None :

            return res

        dd = collections.deque()

        dd.append(root)

        # print(dd)

        while dd :

            sub = []

            for i in range(len(dd)):

                Temp = dd.popleft()

                sub.append(Temp.val)

                if Temp.left:

                    dd.append(Temp.left)

                if Temp.right:

                    dd.append(Temp.right)

            res.append(sub)

        return res
```
Using the stack 
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

        res = []

        temp = []

        temp.append(root)

        if root == None :

            return res

        while temp:

            curr = temp.pop()

            res.append(curr.val)        

            if curr.right:

                temp.append(curr.right)

            if curr.left:

                temp.append(curr.left)

        return res
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