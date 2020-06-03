# 23. Merge k Sorted Lists

Author: LIU Zhuofei  
Date: 2020.6.2  
Rating: 4.5/5.0  

## Problem

Merge k sorted linked lists and return it as one sorted list. Analyze and describe its complexity.  
Example:  
```
Input:
[
  1->4->5,
  1->3->4,
  2->6
]
Output: 1->1->2->3->4->4->5->6
```

## Divide and Conquer

1. Pair up **k** lists and merge each pair.

2. After the first pairing, **k** lists are merged into **k/2** lists with average **2N/k** length.

3. Repeat this procedure until we get the final sorted linked list.

Thus, we'll traverse almost **N** nodes per pairing and merging, and repeat this procedure about **logk** times.

Time Complexity: O(Nlogk)

## Priority Queue (HEAP)

```python
from Queue import PriorityQueue

class Solution(object):
    def mergeKLists(self, lists):
        """
        :type lists: List[ListNode]
        :rtype: ListNode
        """
        head = point = ListNode(0)
        q = PriorityQueue()
        for l in lists:
            if l:
                q.put((l.val, l))
        while not q.empty():
            val, node = q.get()
            point.next = ListNode(val)
            point = point.next
            node = node.next
            if node:
                q.put((node.val, node))
        return head.next
```