# 32. Longest Valid Parentheses (Unfinished)

Author: LIU Zhuofei  
Date: 2020.6.9  

## Problem
Given a string containing just the characters '(' and ')', find the length of the longest valid (well-formed) parentheses substring.

Example 1:
```
Input: "(()"
Output: 2
Explanation: The longest valid parentheses substring is "()"
```

## Dynamic Programming

dp[i] = the number of length ends in index i.

Two cases:
```
1. () dp[i] = dp[i-2]+2
2. (...)) dp[i] = dp[i-1] + dp[i-dp[i-1]-2] + 2 
```

Time complexity: O(n)  

## Stack  

## Two Scan

Example figures help understanding.

[Source](https://leetcode.com/problems/longest-valid-parentheses/solution/)  

(Unfinished)