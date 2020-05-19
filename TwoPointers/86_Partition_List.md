# 86. Partition List

2020/05/19 ZLY

### Problem Description

Given a linked list and a value *x*, partition it such that all nodes less than *x* come before nodes greater than or equal to *x*.

You should preserve the original relative order of the nodes in each of the two partitions.

**Example:**

```python
Input: head = 1->4->3->2->5->2, x = 3
Output: 1->2->2->4->3->5
```

### Algorithm

We maintain two linked list and use two pointers `small`, `large` to keep track of them. Then we traverse through the original linked list, when the node's value is smaller than `x`, we add it to the `small` linked list; otherwise, we add it to the 'large' linked list.

Once we are done with all the nodes in the original linked list, we just need to join the `small` and `large` linked lists.

At first, we will add an auxiliary "dummy" node, which points to the list head. It can be used to deal with some corner cases such as a list with only one node, or removing the head of the list.

For the two pointers, the first pointer starts from the n+1 node and the second pointer starts from the beginning (the dummy node). And they all step by 1 each time until the first pointer points to `None`. That is, we always maintain n-nodes apart between these two pointers. And when the proceeding stops, we can just let `second.next` to point to `second.next.next`.

### Code

```python
def partition(self, head: ListNode, x: int) -> ListNode:
    small = small_head = ListNode()
    large = large_head = ListNode()
    while head:
        if head.val<x:
            small.next = head
            small = small.next
        else:
            large.next = head
            large = large.next
        head = head.next
    large.next = None
    small.next = large_head.next
        
    return small_head.next
```