# 98. Validate Binary Search Tree

2020/05/25 ZLY

### Problem Description

Given a binary tree, determine if it is a valid binary search tree (BST).

Assume a BST is defined as follows:

- The left subtree of a node contains only nodes with keys **less than** the node's key.
- The right subtree of a node contains only nodes with keys **greater than** the node's key.
- Both the left and right subtrees must also be binary search trees.



### Algorithm 1

We can solve this problem recursively. We compare the root node with the lower and upper limit to validate it. And then we recursively repeat the steps for the left subtree and right subtree.

### Code

```python
def isValidBST(self, root: TreeNode) -> bool:
    def helper(node, min_value=float('-inf'),max_value=float('inf')):
        if not node:
            return True
        if node.val <= min_value or node.val >= max_value:
            return False
        return helper(node.left,min_value,node.val) and helper(node.right,node.val,max_value)
    return helper(root)
```



### Algorithm 2

We can traverse this tree by inorder since the nodes of a valid binary search tree in this order will have a increasing order.

### Code

```python
def isValidBST(self, root: TreeNode) -> bool:
    stack, inorder = [], float('-inf')
        
    while stack or root:
        while root:
            stack.append(root)
            root = root.left
        root = stack.pop()
        if root.val <= inorder:
            return False
        inorder = root.val
        root = root.right

    return True
```

