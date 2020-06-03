# 24. Swap Nodes in Pairs

Author: LIU Zhuofei  
Date: 2020.6.3  
Rating: 3.0/5.0  

## Problem
Given a linked list, swap every two adjacent nodes and return its head.

You may not modify the values in the list's nodes, only nodes itself may be changed.

Example:
```
Given 1->2->3->4, you should return the list as 2->1->4->3.
```

## Solution

It's easy to consider one pair as unit to use a loop to swap the nodes. Python gives good code to make use of ```self```
```python
def swapPairs(self, head):
    pre, pre.next = self, head
    while pre.next and pre.next.next:
        a = pre.next
        b = a.next
        pre.next, b.next, a.next = b, a, b.next
        pre = a
    return self.next
```

Maybe one better way is to reduce the condition? I cannot achieve that.

Another is to use recursion. Swap one pair and consider remaining list as new list to call swapPairs function again and again.