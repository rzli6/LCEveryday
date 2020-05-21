### 230. Kth Smallest Element in a BST
LC link: https://leetcode.com/problems/kth-smallest-element-in-a-bst/  
Code: https://colab.research.google.com/drive/1zwh7pppur0pIoEgi3mNOI3cRV9GBBZ0E?usp=sharing  
Author: Ruizhe Li  
Date: 05/20/2020

#### Solution:
LVR of a binary tree is a sorting list. Thus we just need to move k steps to get the number.

#### Code:
```python
# Solution

# Definition for a binary tree node.
# class TreeNode:
#  def __init__(self, val=0, left=None, right=None):
#    self.val = val
#    self.left = left
#    self.right = right

class Solution:
  def kthSmallest(self, root: TreeNode, k: int) -> int:
    self.k = k
    self.helper(root)
    return self.ans
  
  def helper(self, node):
    if not node or self.k < 1:
      return
    self.helper(node.left)
    if self.k == 1:
      self.ans = node.val
    self.k -= 1
    self.helper(node.right)
```