# 129. Sum Root to Leaf Numbers

Author: Xiangde Zeng, 2020.6.1

## Problem

Given a binary tree containing digits from 0-9 only, each root-to-leaf path could represent a number.

An example is the root-to-leaf path 1->2->3 which represents the number 123.

Find the total sum of all root-to-leaf numbers.

Note: A leaf is a node with no children.

Example:
```
Input: [1,2,3]
Output: 25

    1
   / \
  2   3

Explanation:

The root-to-leaf path 1->2 represents the number 12.
The root-to-leaf path 1->3 represents the number 13.
Therefore, sum = 12 + 13 = 25.
```

## Idea
Solution:
DFS: Pass the current value to the next node. Everytime we pass the next node, multiple the value by 10 and do the dfs to the left node and right node. Sum the valuus from the two child nodes to get the answer.


```Java
class Solution {
    public int sumNumbers(TreeNode root) {
        return getSum(root,0);
    }
    
    int getSum(TreeNode node, int sum){
        if(node == null) return 0;
        int num = sum * 10 + node.val;
        if(node.left == null && node.right == null) return num;
        int left = getSum(node.left,num);
        int right = getSum(node.right,num);
        return left + right;
    }
}
```