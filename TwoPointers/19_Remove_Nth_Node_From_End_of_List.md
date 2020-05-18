# 19. Remove Nth Node From End of List

2020/05/13 ZLY

### Problem Description

Given a linked list, remove the *n*-th node from the end of list and return its head.

### Algorithm

To solve the problem in one pass, we can use two pointers. 

At first, we will add an auxiliary "dummy" node, which points to the list head. It can be used to deal with some corner cases such as a list with only one node, or removing the head of the list.

For the two pointers, the first pointer starts from the n+1 node and the second pointer starts from the beginning (the dummy node). And they all step by 1 each time until the first pointer points to `None`. That is, we always maintain n-nodes apart between these two pointers. And when the proceeding stops, we can just let `second.next` to point to `second.next.next`.

### Code

```python
def removeNthFromEnd(self, head: ListNode, n: int) -> ListNode:
        dummy = ListNode()
        dummy.next = head
        first = dummy
        second = dummy
        for i in range(n+1):
            first = first.next
        while first:
            first = first.next
            second = second.next
        second.next = second.next.next
        return dummy.next
```