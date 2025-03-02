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