# 72. Edit Distance

Author: LIU Zhuofei  
Date: 2020.6.17  

## Problem
Given two words word1 and word2, find the minimum number of operations required to convert word1 to word2.

You have the following 3 operations permitted on a word:

Insert a character
Delete a character
Replace a character
```
Example:

Input: word1 = "horse", word2 = "ros"
Output: 3
Explanation: 
horse -> rorse (replace 'h' with 'r')
rorse -> rose (remove 'r')
rose -> ros (remove 'e')
```

## my idea

It must be a DP problem since we need to record state of convertion. But how? Can the operations become states?

No. For any char in word1, we can have 4 operations: insert, delete, replace or do nothing. Note if we do operations, we need to store new word.  

A general idea is to use use dp[i][j] = MinOperations(word1[:i], word2[:j])

The following resource gives a more detailed intuition. Good to have a look.

[Python solutions and intuition](https://leetcode.com/problems/edit-distance/discuss/159295/Python-solutions-and-intuition)  