# 115. Distinct Subsequences

Author: zhuofei  
Date: 2020.5.27  
Rating: 5.0/5.0  

## Problem  
Given a string S and a string T, count the number of distinct subsequences of S which equals T.

A subsequence of a string is a new string which is formed from the original string by deleting some (can be none) of the characters without disturbing the relative positions of the remaining characters. (ie, "ACE" is a subsequence of "ABCDE" while "AEC" is not).

It's guaranteed the answer fits on a 32-bit signed integer.

Example:
```
Input: S = "babgbag", T = "bag"
Output: 5
Explanation:
As shown below, there are 5 ways you can generate "bag" from S.
(The caret symbol ^ means the chosen letters)

babgbag
^^ ^
babgbag
^^    ^
babgbag
^    ^^
babgbag
  ^  ^^
babgbag
    ^^^
```

## My idea

1. toCharArray string S and T.  
2. hashmap to record indexs of each character of T in string S, e.g. first char **b** of T appear in index 0,2,4 in string S in above example.  
3. Then it will be a problem to create an array from small number to large number

Time Complexity: O(n^m)


## Dynamic Programming
1. dp[i][j]:
   1. i means substring(0, i) of S
   2. j meams substring(0, j) of T
   3. dp[i][j] = numDistinct(S.substring(0,i), T.substring(0,j));
   4. dp[i+1][j+1] = dp[i][j] + dp[i+1][j](if T[i] == S[j], otherwise only dp[i][j])
   5. dp[S.length()][T.length()] is the result
   
## Better result
[Source](https://leetcode.wang/leetcode-115-Distinct-Subsequences.html)