# 10. Regular Expression Matching

Author: LIU Zhuofei  
Date: 2020.5.29  
Rating: 3.5/5.0 Very Difficult!  

## Problem
Given an input string (s) and a pattern (p), implement regular expression matching with support for '.' and '*'.

The matching should cover the entire input string (not partial).

Example:
```
Input:
s = "mississippi"
p = "mis*is*p*."
Output: false
```

## Idea

I cannot solve it ny myself. It's better for me to recite solution and save my life. The answer is beautiful.  

### Recursive
```
class Solution {
    public boolean isMatch(String text, String pattern) {
        if (pattern.isEmpty()) return text.isEmpty();
        boolean first_match = (!text.isEmpty() &&
                               (pattern.charAt(0) == text.charAt(0) || pattern.charAt(0) == '.'));

        if (pattern.length() >= 2 && pattern.charAt(1) == '*'){
            // first is * matches 0 times
            // second is * macthes multiple times
            // idea is match one by one! I don't get it when I code.
            return (isMatch(text, pattern.substring(2)) ||
                    (first_match && isMatch(text.substring(1), pattern)));
        } else {
            // no *
            return first_match && isMatch(text.substring(1), pattern.substring(1));
        }
    }
}
```
### DP

[Solution](https://leetcode.com/problems/regular-expression-matching/discuss/5651/Easy-DP-Java-Solution-with-detailed-Explanation)
