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