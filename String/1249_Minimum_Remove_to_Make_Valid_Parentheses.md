### 1249. Minimum Remove to Make Valid Parentheses
Link: https://leetcode.com/problems/minimum-remove-to-make-valid-parentheses/  
Author: Xiangde Zeng  
Date: 06/23/2020  

### Question
Given a string s of `'('` , `')'` and lowercase English characters. 

Your task is to remove the minimum number of parentheses ( `'('` or `')'`, in any positions ) so that the resulting *parentheses string* is valid and return **any** valid string.

Formally, a *parentheses string* is valid if and only if:

- It is the empty string, contains only lowercase characters, or
- It can be written as `AB` (`A` concatenated with `B`), where `A` and `B` are valid strings, or
- It can be written as `(A)`, where `A` is a valid string.

**Example:**  
```
Input: s = "lee(t(c)o)de)"
Output: "lee(t(c)o)de"
Explanation: "lee(t(co)de)" , "lee(t(c)ode)" would also be accepted.
```
#### Solution: 
Set + stack

```java
class Solution {
    public String minRemoveToMakeValid(String s) {
        Set<Integer> rm_idx = new HashSet<Integer>();
        Stack<Integer> st = new Stack<Integer>();
        for(int i = 0;i<s.length();i++){
            if(s.charAt(i) == '(') st.push(i);
            if(s.charAt(i) == ')'){
                if(st.isEmpty()) rm_idx.add(i);
                else st.pop();
            }
        }
        StringBuilder sb = new StringBuilder();
        while(!st.isEmpty()) rm_idx.add(st.pop());
        for(int i = 0;i<s.length();i++){
            if(rm_idx.contains(i)) continue;
            sb.append(s.charAt(i));
        }
        return sb.toString();
    }
}
```