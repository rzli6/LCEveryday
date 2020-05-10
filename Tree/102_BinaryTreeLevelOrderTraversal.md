# 102. Binary Tree Level Order Traversal

## Problem
Given a binary tree, return the level order traversal of its nodes' values. (ie, from left to right, level by level).  
Example:  
```
    3
   / \
  9  20
    /  \
   15   7
```
Result:
```
[
  [3],
  [9,20],
  [15,7]
]
```

## Problem-solving ideas (老刘)
First idea: BFS  
Main problem focuses on how to differ levels of binary tree.  
So I use two queues to record current level of TreeNodes and next level of TreeNodes respectively.  
How to improve it? I do not need to use another queue. It's easy to firstly record the size of queue, and loop the queue in that size.
