### 1008. Construct Binary Search Tree from Preorder Traversal
LC link: https://leetcode.com/problems/construct-binary-search-tree-from-preorder-traversal/submissions/
Code: https://colab.research.google.com/drive/1zwh7pppur0pIoEgi3mNOI3cRV9GBBZ0E?usp=sharing  
Author: Ruizhe Li  
Date: 05/26/2020

#### Solution:
Key point: In-order traversal result of a Binary Search Tree is increasing/sorted.  
We can use the in-order and pre-order to construst a tree.  
Here we provide another possibility with recursion. Intuitively, when encounter a number, it could be left or right of the current node, and it all depends on their values to determine left right or parent.
* If the child value is smaller than the current node, it is a left child
* If the child value is larger than the current node:
  * if the child value is smaller than the parent of current node, then it is the right child of current node
  * if the child value is larger than the parent of current node, then it must be in the right of parent node, we adjust the parent node one level up.

#### Code:
```python
# Definition for a binary tree node.
# class TreeNode:
  # def __init__(self, val=0, left=None, right=None):
  #   self.val = val
  #   self.left = left
  #   self.right = right
class Solution:
  def __init__(self):
    self.i = 0
  def bstFromPreorder(self, preorder: List[int], bound = 1e9) -> TreeNode:
    # if reach the end of preorder list
    # or if the current value is larger than the bound
    # the current value must not a child in this interval
    # we return without touching the current value
    if self.i == len(preorder) or preorder[self.i] > bound:
      return None
    
    # if the node is in this interval
    # then we construct the node and move forward
    node = TreeNode(preorder[self.i])
    self.i += 1

    # set a new boundary for its left node
    node.left = self.bstFromPreorder(preorder, bound=node.val)
    
    # the upper bound will not be changed for its right child
    node.right = self.bstFromPreorder(preorder, bound)

    return node
```                
