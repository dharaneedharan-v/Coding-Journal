## Singly 
### Count Linked List Nodes : 

```PYTHON 
'''
#Linked list class
class LinkedList:
    def __init__(self):
        self.head=None
        self.tail=None
        '''

class Solution:
    # Function to count nodes of a linked list.
    def getCount(self, head):
        # code here
        count = 0 
        temp = head 
        while temp.next :
            count = count +  1
            temp = temp.next 
        return count +1 
```

### [Remove Duplicates from Sorted List](https://leetcode.com/problems/remove-duplicates-from-sorted-list/)


```python 
# Definition for singly-linked list.

# class ListNode:

#     def __init__(self, val=0, next=None):

#         self.val = val

#         self.next = next

class Solution:

    def deleteDuplicates(self, head: Optional[ListNode]) -> Optional[ListNode]:

        temp= head

        if not head :

            return None

        while temp and temp.next :

            if temp.val == temp.next.val:

                temp.next = temp.next.next

            else :

                temp = temp.next

        return head
```


### Search in Linked List : 

```python 

 ''' Node of a linked list
class Node:
    def __init__(self, data):
        self.data = data
        self.next = None
'''
class Solution:
    def searchKey(self, n, head, key):
        #Code here
        temp = head 
        while temp.next :
            if temp.data == key:
                return True 
            temp = temp.next
        return False 
```


### Middle of a Linked List: 

```python 

class Solution:
    #  Should return data of middle node. If linked list is empty, then  -1
    def getMiddle(self, head):
        
        count = 0
        check = 0 
        temp = head
        while temp:
            count = count + 1 
            temp = temp.next
        print(count)
        count = count //2 
        print(count)
        # Important or Hint :
        # temp should be reassigned other wise it will point to the tail or none null
        temp = head 
        while temp :
            if check == count:
                return temp.data
                # print(temp.data)
            check =check + 1
            temp = temp.next
        
```
### Delete in a Singly Linked List : 

```python 
def deleteNode(head, x):
    if head is None :
        return None 
        
    if  x == 1 :
        return head.next
        
    count = 0 
    temp = head 
    while temp.next:
       count = count + 1
       if count == x-1 :
           if temp.next is not None:  # Ensure there is a node to delete
                temp.next = temp.next.next
        #   temp.next = temp.next.next 
           return head
        #   print(temp.data)
       temp = temp.next
    # print(count)
    return head 

```

### Linked List Insertion At End : 

```python 
class Solution:
    #Function to insert a node at the end of the linked list.
    def insertAtEnd(self,head,x):
        dd = Node(x)
        temp = head 
        if head == None :
            return dd
        while temp.next :
            temp = temp.next
        temp.next = dd
        return head 

```

### [206. Reverse Linked List](https://leetcode.com/problems/reverse-linked-list/)

INTERVIEWER NOT LIKE THIS ANSWER : 

```python # Definition for singly-linked list.

# class ListNode:

#     def __init__(self, val=0, next=None):

#         self.val = val

#         self.next = next

class Solution:

    def reverseList(self, head: Optional[ListNode]) -> Optional[ListNode]:

        temp = head

        dd = []

        while temp :

            dd.append(temp.val)

            temp = temp.next

            # reinitialize the temp because it will point to null it traversed to last and  pointing to null value currently.

        temp = head

        while temp :

            temp.val = dd.pop()

            temp = temp.next

        return head
        
```

### [234. Palindrome Linked List](https://leetcode.com/problems/palindrome-linked-list/) 

INTERVIEWER NOT LIKE THIS ANSWER : 
```python 
# Definition for singly-linked list.

# class ListNode:

#     def __init__(self, val=0, next=None):

#         self.val = val

#         self.next = next

class Solution:

    def isPalindrome(self, head: Optional[ListNode]) -> bool:

        dd =[]

        if not head :

            return None

        temp = head

        while temp :

            dd.append(temp.val)

            print(temp.val)

            temp = temp.next

        return dd == dd[::-1]

```

### [19. Remove Nth Node From End of List](https://leetcode.com/problems/remove-nth-node-from-end-of-list/)

INTERVIEWER NOT LIKE THIS ANSWER : 
```python 
# Definition for singly-linked list.

# class ListNode:

#     def __init__(self, val=0, next=None):

#         self.val = val

#         self.next = next

class Solution:

    def removeNthFromEnd(self, head: Optional[ListNode], n: int) -> Optional[ListNode]:

        temp = head

        dd =[]

        count = 1

        while temp :

            count = count +1

            dd.append(temp.val)

            print(temp.val)

            temp = temp.next

        dd.pop(-(n))

        if not dd :

            return None

        head = ListNode(dd[0])

        temp = head

        for i in range(1,len(dd)):

            temp.next = ListNode(dd[i])

            temp = temp.next

        return head
```

### [92. Reverse Linked List II](https://leetcode.com/problems/reverse-linked-list-ii/)

INTERVIEWER NOT LIKE THIS ANSWER : 
```python 
# Definition for singly-linked list.

# class ListNode:

#     def __init__(self, val=0, next=None):

#         self.val = val

#         self.next = next

class Solution:

    def reverseBetween(self, head: Optional[ListNode], left: int, right: int) -> Optional[ListNode]:

        temp = head

        dd = []

        while temp :

            dd.append(temp.val)

            temp = temp.next

        # print(dd)

        if left <= right:

            start = left - 1  

            end = right - 1  

            dd[:] = dd[:start] + dd[start:end+1][::-1] + dd[end+1:]

            print(dd)

        if not dd :

            return None

        head = ListNode(dd[0])

        temp = head

        for i in range(1,len(dd)):    

            temp.next = ListNode(dd[i])        

            temp = temp.next

        return head
```

### [141. Linked List Cycle](https://leetcode.com/problems/linked-list-cycle/)

```python 
# Definition for singly-linked list.

# class ListNode:

#     def __init__(self, x):

#         self.val = x

#         self.next = None

  

class Solution:

    def hasCycle(self, head: Optional[ListNode]) -> bool:

        if not head  :

            return False

        fast = head

        slow = head

        # Instead of using the temp , use the fast, fast.next.next becomes  None so we get error

        while fast and fast.next :

            slow = slow.next

            fast = fast.next.next

            if (fast ==  slow ):

                return True

        return False
```
## Double LinkedList

### Introduction to Doubly Linked List

1) Construct the doubly linked list from **arr**

```python 
'''
# Node Class
	class Node:
	    def __init__(self, data):   # data -> value stored in node
	        self.data = data
	        self.next = None
	        self.prev = None

'''
class Solution:
    def constructDLL(self, arr):
        if len(arr)== 0 :
            return None 
        head =Node(arr[0])
        temp = head
        for i in range(1,len(arr)):
            dd = Node(arr[i])
            temp.next = dd
            dd.prev  = temp
            temp = dd
        return head
```

###  Reverse A Doubly Linked List

```python 
'''
class DLLNode:
    def __init__(self, val):
        self.data = val
        self.next = None
        self.prev = None
'''

class Solution:
    def reverseDLL(self, head):
        #return head of reverse doubly linked list
        #TC-> O(N)
        #TC-> O(2N)
        dd =[]
        temp = head 
        while temp :
            dd.append(temp.data)
            temp = temp.next
        # Need to be reinitzatlise the temp 
        temp = head 
        # return head 
        while temp :
            temp.data=dd.pop()
            temp = temp.next
        return head
```

```python 
'''
class DLLNode:
    def __init__(self, val):
        self.data = val
        self.next = None
        self.prev = None
'''

class Solution:
    def reverseDLL(self, head):
         # Return head of reversed doubly linked list
        # TC -> O(N)
        # SC -> O(1)  (in-place reversal, not O(2N))
        if not head :
            return None
        if head.next is None :
            return head 
        temp = head 
        last = None 
        while temp :
            last = temp.prev
            temp.prev = temp.next
            temp.next = last 
            
        # Move to the next node (which is in temp.prev now)
 
            temp  = temp.prev
        return  last.prev
```

### [21. Merge Two Sorted Lists](https://leetcode.com/problems/merge-two-sorted-lists/)

Not optimal solution 

```python 
# Definition for singly-linked list.

# class ListNode:

#     def __init__(self, val=0, next=None):

#         self.val = val

#         self.next = next

class Solution:

    def mergeTwoLists(self, list1: Optional[ListNode], list2: Optional[ListNode]) -> Optional[ListNode]:

        dd = []

        temp1 = list1

        temp2 = list2

        while temp1 :

            dd.append(temp1.val)

            print(temp1.val)

            temp1 = temp1.next

  

        while temp2 :

            dd.append(temp2.val)

            temp2 = temp2.next

        dk = sorted(dd)

        if not dk :

            return None

        head = ListNode(dk[0])

        temp = head

        for i in dk[1:]:

            temp.next = ListNode(i)

            temp = temp.next

        return head
```


### [160. Intersection of Two Linked Lists](https://leetcode.com/problems/intersection-of-two-linked-lists/)

BRUTE FORCE SPACE 
```python 
# Definition for singly-linked list.

# class ListNode:

#     def __init__(self, x):

#         self.val = x

#         self.next = None

  

class Solution:

    def getIntersectionNode(self, headA: ListNode, headB: ListNode) -> Optional[ListNode]:

        dd = {}

        temp = headA

        while temp :

            if temp not in dd :

                dd[temp] = 1

            temp = temp.next

        temp1 = headB

        while temp1 :

            if temp1 in dd :

                return temp1

            temp1 = temp1.next

        return None
```

Using the Traversal Alone : For the O(1 ) space

```python 
# Definition for singly-linked list.

# class ListNode:

#     def __init__(self, x):

#         self.val = x

#         self.next = None

  

class Solution:

    def getIntersectionNode(self, headA: ListNode, headB: ListNode) -> Optional[ListNode]:

        # If either of the lists is empty, there is no intersection.

        if headA is None or headB is None:

            return None

  

        # Create two pointers, one for each linked list.

        pointerA = headA

        pointerB = headB

  

        # Traverse both lists until the two pointers meet.

        while pointerA != pointerB:

            # Move pointerA to the next node in list A.

            # If it reaches the end, switch to the head of list B.

            if pointerA is not None:

                pointerA = pointerA.next

            else:

                pointerA = headB  # Switch to the other list

  

            # Move pointerB to the next node in list B.

            # If it reaches the end, switch to the head of list A.

            if pointerB is not None:

                pointerB = pointerB.next

            else:

                pointerB = headA  # Switch to the other list

  

        # The loop ends when both pointers are equal (either at intersection or None).

        return pointerA  # This is the intersection node or None if no intersection.
```
### [148. Sort List](https://leetcode.com/problems/sort-list/)

SPACE => O(N) 
To be optimized use the Merge sort for this ...!!!
```python 
# Definition for singly-linked list.

# class ListNode:

#     def __init__(self, val=0, next=None):

#         self.val = val

#         self.next = next

class Solution:

    def sortList(self, head: Optional[ListNode]) -> Optional[ListNode]:

        dd = []

        if not head :

            return head

        temp= head

        while temp :

            dd.append(temp.val)

            temp = temp.next

        # print(dd)

        dd.sort()

        # print(dd)

        temp = head

        while temp :

            temp.val = dd.pop(0)

            temp= temp.next

        return head
```

### Sort a linked list of 0s, 1s and 2s


Solved using the Another list and sorted and returned -----------> Time Limit Exceeded  

Now , By Taking the count of the 0 1 and 2 and rewrite the data in the nodes 
```python 
class Solution:
    #Function to sort a linked list of 0s, 1s and 2s.
    def segregate(self, head):
        if not head:
            return None
        dd = [0, 0 ,0]
        temp = head
        while temp :
            dd[temp.data] += 1 
            temp = temp.next 
        # print(dd)
        temp = head 
        for i in range(len(dd)):
            while dd[i] > 0 :
                temp.data = i
                temp  =temp.next 
                dd[i] -= 1 
        return head 
```


### Add 1 to a Linked List Number


Not optimized one use the recursion to it in a optimized way 


```python 

class Solution:
    def addOne(self,head):
        dd  = []
        if not head :
            return None 
        temp = head 
        while temp :
            dd.append(temp.data)
            temp = temp.next 
        # print(dd)
        
        def add(dd):
            for i in range(len(dd)-1,-1,-1):
                if dd[i] < 9  :
                    dd[i] += 1 
                    return dd
                dd[i] =0 
            return [1]+dd
            
        def create(dd):
            head = Node(dd[0])
            temp = head 
            for i in range(1,len(dd)):
                new = Node(dd[i])
                temp.next = new 
                temp = new  
            return head
        
        Add = add(dd)
        return create(Add)
```

### [25. Reverse Nodes in k-Group](https://leetcode.com/problems/reverse-nodes-in-k-group/)

```python 
# Definition for singly-linked list.

# class ListNode:

#     def __init__(self, val=0, next=None):

#         self.val = val

#         self.next = next

class Solution:

    def reverseKGroup(self, head: Optional[ListNode], k: int) -> Optional[ListNode]:

        if not head or k <= 1:

            return head  # No change needed

  

        # Step 1: Convert Linked List to List

        temp = head

        dd = []

        while temp:

            dd.append(temp.val)

            temp = temp.next

        print("Original List:", dd)

  

        # Step 2: Reverse every k elements

        def rev(dd, k):

            dk = []

            for i in range(0, len(dd), k):

                chunk = dd[i:i+k]

                if len(chunk) == k:  # Only reverse if a full k-group

                    dk.extend(chunk[::-1])

                else:

                    dk.extend(chunk)  # Append remaining as is

            return dk

  

        # Step 3: Reconstruct the Linked List

        def create(dk, head):

            temp = head

            index = 0  # Use indexing instead of pop(0) for efficiency

            while temp:

                temp.val = dk[index]

                temp = temp.next

                index += 1

            return head

  

        Rev = rev(dd, k)

        print("Reversed List:", Rev)

        return create(Rev, head)
```




### [61. Rotate List](https://leetcode.com/problems/rotate-list/)


```python 
# Definition for singly-linked list.

# class ListNode:

#     def __init__(self, val=0, next=None):

#         self.val = val

#         self.next = next

class Solution:

    def rotateRight(self, head: Optional[ListNode], k: int) -> Optional[ListNode]:

        temp = head

        dd= []

        if not head :

            return None

        while temp :

            dd.append(temp.val)

            temp = temp.next

        def rotate(dd, k):

            if  k >= len(dd):

                k = k%len(dd)

            return dd[-k:]+ dd[:-k]

        def create (dd):

            temp = head

            for i in dd :

                temp.val = i

                temp = temp.next

            return head

        Rot = rotate(dd,k)

        Create = create(Rot)

        return Create
```


### [23. Merge k Sorted Lists](https://leetcode.com/problems/merge-k-sorted-lists/)


Brute Force : 

```python 
# Definition for singly-linked list.

# class ListNode:

#     def __init__(self, val=0, next=None):

#         self.val = val

#         self.next = next

class Solution:

    def mergeKLists(self, lists: List[Optional[ListNode]]) -> Optional[ListNode]:

        lenght = len(lists)

        if lists is None :

            return []

        dd = []

        for i in range(lenght):

            temp = lists[i]

            while temp :

                dd.append(temp.val)

                temp = temp.next        

        Sort = sorted (dd)

        if Sort is None or len(Sort) == 0 : 

            return None

        head = ListNode(Sort[0])

        temp = head  # intialize the temp for the traversal 

        for i in range(1,len(Sort)):

            Node = ListNode(Sort[i])

            temp.next = Node

            temp = temp.next

        return head
```

