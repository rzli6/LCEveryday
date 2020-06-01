# 22. Generate Parentheses

Author: LIU Zhuofei  
Date: 2020.5.31  
Rating: 4.0/5.0  

## Problem

Given n pairs of parentheses, write a function to generate all combinations of well-formed parentheses.

For example, given n = 3, a solution set is:
```
[
  "((()))",
  "(()())",
  "(())()",
  "()(())",
  "()()()"
]
```

## Backtracking

Backtracking is an algorithmic-technique for solving problems recursively by trying to build a solution incrementally, one piece at a time, removing those solutions that fail to satisfy the constraints of the problem at any point of time (by time, here, is referred to the time elapsed till reaching any level of the search tree).  

## Idea

I consider it as recursive and backtracing problem. If we see String as a tree, it's also a DFS problem.  

We should ensure the number of '(' is larger than ')' when we adding parenthesis to string.

## Code

```
public List<String> generateParenthesis(int n) {
    List<String> ans = new ArrayList();
    backtrack(ans, "", 0, 0, n);
    return ans;
}

public void backtrack(List<String> ans, String cur, int left, int right, int n){
    if (cur.length() == n * 2) {
        ans.add(cur);
        return;
    }
    //左括号不要超过 n
    if (left < n)
        backtrack(ans, cur+"(", left+1, right, n);
    //右括号不要超过左括号
    if (right < left)
        backtrack(ans, cur+")", left, right+1, n);
}
```