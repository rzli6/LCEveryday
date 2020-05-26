### 328. Odd Even Linked List
LC link: https://leetcode.com/problems/odd-even-linked-list/  
Code: https://colab.research.google.com/drive/1zwh7pppur0pIoEgi3mNOI3cRV9GBBZ0E?usp=sharing  
Author: Ruizhe Li  
Date: 05/26/2020

#### Solution:
* Break the single list to two separate lists. 
One for odd entries and the other for even entries.  
* Append the even list at the end of odd list

#### Code:
```python
# Definition for singly-linked list.
# class ListNode:
  # def __init__(self, val=0, next=None):
  #   self.val = val
  #   self.next = next
class Solution:
  def oddEvenList(self, head: ListNode) -> ListNode:
    # if the list contains 2 items only, directly return.
    if not head or not head.next:
      return head
    
    # the current pointers for odd and even item
    # the head node for even list
    odd, even, evenHead = head, head.next, head.next

    # breaking
    while even and even.next:
      odd.next = even.next
      odd = odd.next
      even.next = odd.next
      even = even.next

    # merging 
    odd.next = evenHead
    return head
```