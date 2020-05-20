# 61. Rotate List

2020/05/20 ZLY

### Problem Description

Given a linked list, rotate the list to the right by *k* places, where *k* is non-negative.

**Example 1:**

```
Input: 1->2->3->4->5->NULL, k = 2
Output: 4->5->1->2->3->NULL
Explanation:
rotate 1 steps to the right: 5->1->2->3->4->NULL
rotate 2 steps to the right: 4->5->1->2->3->NULL
```

**Example 2:**

```
Input: 0->1->2->NULL, k = 4
Output: 2->0->1->NULL
Explanation:
rotate 1 steps to the right: 2->0->1->NULL
rotate 2 steps to the right: 1->2->0->NULL
rotate 3 steps to the right: 0->1->2->NULL
rotate 4 steps to the right: 2->0->1->NULL
```

### Algorithm 1

We first traverse the list to get the length of the linked list. Then we connect the `head` node and `tail` node. Finally, we traverse towards the new `head` node, break the list (i.e. make it point to `None`)

### Code 1

```python
def rotateRight(self, head: ListNode, k: int) -> ListNode:
    if not head:
        return head
    start = head
    length = 1
    while start.next:
        start = start.next
        length += 1
    if length<=1:
        return head
    step = k%length
    if step == 0:
        return head
    start.next = head
    step = length - step
    while step:
        start = start.next
        step -= 1
    result = start.next
    start.next = None
    return result
            
```



### Algorithm 2

We also first get the length of the list. Then we use two pointers `slow` and `fast`. The `fast` pointer will first move `k` steps. Then both pointers move together by 1 each time. When the `fast` pointer reach the tail, the `slow` pointer would point to the new head node. 

### Code 2

```python
def rotateRight(self, head, k):
    if not head or not head.next or k==0:
        return head
    ListLen = 0
    p = head
    #数有几个节点
    while(p):
        ListLen+=1
        p = p.next
            
    #优化
    k = k%ListLen
    if k==0:
        return head
        
    #快节点先走k步
    p = head
    while(k>0):
        k -=1
        p = p.next
    slow = head
    fast = p
    #接着让fast走到最后一个节点，slow与它有着同样的速度
    while fast.next:
        slow = slow.next
        fast = fast.next
        
    #把头尾连起来然后断开链表
    new_head = slow.next 
    fast.next = head
    slow.next = None
    return new_head
```



*Corner cases: empty linked list / length equals 1 / step is multiple of length. (We should all return the original list)