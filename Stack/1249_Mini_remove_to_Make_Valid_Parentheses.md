### [1249. Minimum Remove to Make Valid Parentheses](https://leetcode.com/problems/minimum-remove-to-make-valid-parentheses/)
Author: Ruizhe Li  
Date: 06/02/2020

#### Solution:
An elegent way to simulate the parentheses construction with stack.

#### Code:
```python
class Solution:
  def minRemoveToMakeValid(self, s: str) -> str:
    stk, cur = [], ''
    for c in s:
      if c == '(':
        stk.append(cur)
        cur = ''
      elif c == ')':
        if stk:
          # next sequence to be included in a paratheness
          cur = stk.pop() + '(' + cur + ')'
      else:
        # append the char to current sequence
        cur += c

    while stk:
      # empty the stack
      cur = stk.pop() + cur
    return cur
```