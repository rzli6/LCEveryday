#  92. Reverse Linked List II

2020/05/11 ZLY

### Problem Description

Reverse a linked list from position *m* to *n*. Do it in one-pass.

**Note:** 1 ≤ *m* ≤ *n* ≤ length of list.

### Algorithm

1. Let's say we have a linked list consisting of three different nodes, `A → B → C` and we want to reverse the links between the nodes and obtain `A ← B ← C`. If we have a pointer `prev` pointing to node `A` and another pointer `cur` pointing to node `B`, then we can simply achieve this by

   ```
   cur.next = prev
   ```

   The only problem with this is, we don't have a way of progressing further i.e. once we do this, we can't reach the node `C`. That's why we need a third pointer that will help us continue the link reversal process. So, we do the following instead.

   ```python
   nextp = cur.next
   cur.next = prev
   prev = cur
   cur = nextp
   ```

2. Once we finish reversing `A → B → C ` , final step is to manage the head and tail connection. For example, if the linked list is `start → A → B → C → end`, then in the end, we need to let `start.next = C` and `A.next = end`. Therefore, we need to record these two nodes at first.

   ```python
   cur = head
   prev = None
   for i in range(m-1):
   		prev = cur
       cur = cur.next
   start = prev
   end = cur
   ```

   Here, the variable `start` will represent the node `start` and the variable `end` will represent the node `A` in this example.

   Also, we need to pay attention to the situation when `m=1`. In this case, the `start` variable may become `None`. Then we just need to assign node `C` to `head`.

   ```python
   if start:
       start.next = prev
   else:
       head = prev
   end.next = cur
   ```

   

*Pay attention to special cases: empty list etc.*

```python
if not head:
    return None
```

