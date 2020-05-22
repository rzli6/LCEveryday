# 94. Binary Tree Inorder Traversal

2020/05/22 ZLY

### Problem Description

Given a binary tree, return the *inorder* traversal of its nodes' values.



### Algorithm

Recursively first traverse the left subtree of the root node, then add the value of the root node, finally traverse the right subtree of the root node.

*Note the case when then tree is empty.

Once we are done with all the nodes in the original linked list, we just need to join the `small` and `large` linked lists.

At first, we will add an auxiliary "dummy" node, which points to the list head. It can be used to deal with some corner cases such as a list with only one node, or removing the head of the list.

For the two pointers, the first pointer starts from the n+1 node and the second pointer starts from the beginning (the dummy node). And they all step by 1 each time until the first pointer points to `None`. That is, we always maintain n-nodes apart between these two pointers. And when the proceeding stops, we can just let `second.next` to point to `second.next.next`.

### Code

```python
def inorderTraversal(self, root: TreeNode) -> List[int]:
    if not root:
        return []
    result = []
    result+=self.inorderTraversal(root.left)
    result.append(root.val)
    result+=self.inorderTraversal(root.right)
    return result
```