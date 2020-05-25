# 199. Binary Tree Right Side View

Author: LIU Zhuofei, 2020.5.24

## Problem

Given a binary tree, imagine yourself standing on the right side of it, return the values of the nodes you can see ordered from top to bottom.

Example:
```
Input: [1,2,3,null,5,null,4]
Output: [1, 3, 4]
Explanation:

   1            <---
 /   \
2     3         <---
 \     \
  5     4       <---
```

## Idea
Solution:
1. Level order traversal
2. DFS

If we know about the depth of tree, DFS will be great. Otherwise, level order traversal will be much easier to understand.

The core idea:
1. Only select the rightmost node in each depth of tree
   - It's great to gather all nodes in this depthand add the rightmost one  
2. Current size of result list is current depth.
   - No need to maintain a new variable  

In addition, it's actually similar to Problem [102](https://leetcode.com/problems/binary-tree-level-order-traversal/)
