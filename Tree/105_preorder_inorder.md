# 105. Construct Binary Tree from Preorder and Inorder Traversal

## Problem
Given preorder and inorder traversal of a tree, construct the binary tree.  
Example:
```
preorder = [3,9,20,15,7]
inorder = [9,3,15,20,7]
```
Result:
```
    3
   / \
  9  20
    /  \
   15   7
```
## Note
Mediun Problem But it's easy. **Not Recommended!**

## Ideas (老刘)
Easy to divide it into many sub-problems:
1. find root node
2. divide preorder and inorder array into two parts: left sub-tree and right sub-tree
3. repeat following steps to find node.left and node.right