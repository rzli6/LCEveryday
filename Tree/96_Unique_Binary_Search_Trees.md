# 96. Unique Binary Search Trees

2020/05/24 ZLY

### Problem Description

Given *n*, how many structurally unique **BST's** (binary search trees) that store values 1 ... *n*?



### Algorithm

We can use dynamic programming. Let `G(n)` be the number of binary search trees with `n` nodes and `f(i)` be the number of binary search trees with n nodes and root node `i`. Therefore, we can get that `G(n) = f(1) + f(2) + f(3) +...+ f(n)`.

With `n` nodes and root node `i`, its left subtree has `i-1` nodes and its right subtree has `n-i` nodes. Therefore, we can get that `f(i) = G(i-1)*G(n-i)`.

With these rules, we can get `G(x)` with `x` from `0` to `n`. The base cases are `G(0) G(1) = 1`.

*Note the case when then tree is empty.

Once we are done with all the nodes in the original linked list, we just need to join the `small` and `large` linked lists.

At first, we will add an auxiliary "dummy" node, which points to the list head. It can be used to deal with some corner cases such as a list with only one node, or removing the head of the list.

For the two pointers, the first pointer starts from the n+1 node and the second pointer starts from the beginning (the dummy node). And they all step by 1 each time until the first pointer points to `None`. That is, we always maintain n-nodes apart between these two pointers. And when the proceeding stops, we can just let `second.next` to point to `second.next.next`.

### Code

```python
def numTrees(self, n: int) -> int:
    G = [0]*(n+1)
    G[0] = G[1] = 1
    for i in range(2,n+1):
        for j in range(i):
            G[i] += G[j]*G[i-j-1]
    return G[n]
```