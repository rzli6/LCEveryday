### 143. Reorder List
LC link: https://leetcode.com/problems/reorder-list/  
Author: Ruizhe Li  
Date: 05/10/2020  
Code: https://colab.research.google.com/drive/1zwh7pppur0pIoEgi3mNOI3cRV9GBBZ0E?usp=sharing

#### Solution
Solve with three steps:
1. Find the middle point and split the list to two halves `lst1` and `lst2`.
1. Reverse the second half `lst2` <img src="https://render.githubusercontent.com/render/math?math=\rightarrow"> `reversedLst2`
1. Merge `lst1` and `reversedLst2`

Takeaway:
* Pay attention to corner cases like [ ] and [1]

#### Code:
```python
class Solution:
  def reverseLst(self, head: ListNode) -> ListNode:
    # reverse the given list
    if not head.next:
      return head
    pre, cur = head, head.next
    head.next = None
    while cur:
      tmp = cur.next
      cur.next = pre
      pre = cur
      cur = tmp
    return pre

  def findNSplit(self, head: ListNode) -> ListNode:
    # find the midpoint using fast-slow pointers
    fast, slow = head.next, head
    while fast:
      fast = fast.next
      slow = slow.next
      if fast:
        fast = fast.next
    return slow

  def merge(self, lst1, lst2) -> None:
    # merge two lists
    while lst1 and lst2:
      llst1, llst2 = lst1.next, lst2.next
      lst1.next = lst2
      lst2.next = llst1
      lst1 = llst1
      lst2 = llst2

  def reorderLst(self, head: ListNode) -> None:
    # trivial case: list with 0 or 1 node
    if not head or not head.next:
      return

    # step 1: find midpoint and split the list to two halves
    midNode = self.findNSplit(head)

    # trivial case: nothing to reverse, return original list
    if not midNode or not midNode.next:
      return

    # step 2: reverse the second half
    reversedLst2 = self.reverseLst(midNode.next)
  
    # step 3: merge the two list
    lst1 = head
    midNode.next = None
    self.merge(lst1, reversedLst2)
```