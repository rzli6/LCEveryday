# 222. Count Complete Tree Nodes

Aurthor: LIU Zhuofei, 2020.5.25  
Rating: 4.0/5.0

## Problem

Given a complete binary tree, count the number of nodes.

Note:

Definition of a complete binary tree from Wikipedia:
In a complete binary tree every level, except possibly the last, is completely filled, and all nodes in the last level are as far left as possible. It can have between 1 and 2h nodes inclusive at the last level h.

Example:
```
Input: 
    1
   / \
  2   3
 / \  /
4  5 6

Output: 6
```

## Ideas

divide and conquer:

Get height of left and right sub-tree, if they are equal, compute the result according to height. Otherwise, 
```
RESULT = 1 + countNodes(root.left) + countNodes(root.right)
```

Drawback: please make full use of concept of complete tree.

## Better Solutioin

[Source](https://leetcode.com/problems/count-complete-tree-nodes/discuss/61958/Concise-Java-solutions-O(log(n)2))

## Note

This problem require a deep understanding to a tree and how to divide and conquer. It's great to do it again.