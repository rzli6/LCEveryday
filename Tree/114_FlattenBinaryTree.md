# 114. Flatten Binary Tree to Linked List
Author: 老刘

## Problem
Given a binary tree, flatten it to a linked list in-place.

For example, given the following tree:
```
    1
   / \
  2   5
 / \   \
3   4   6
```
The flattened tree should look like:
```
1
 \
  2
   \
    3
     \
      4
       \
        5
         \
          6
```

## Ideas
Basic idea is to divide into some sub-problems.

The most fundermental problem is a root with one left and one right node. Follow the following steps:

1. store right node
2. change left node to right
3. root.left.right = right (stored)
   
## Resources give more details
[My short post order traversal Java solution for share](https://leetcode.com/problems/flatten-binary-tree-to-linked-list/discuss/36977/My-short-post-order-traversal-Java-solution-for-share)