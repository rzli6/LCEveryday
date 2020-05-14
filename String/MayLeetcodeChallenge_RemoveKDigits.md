### May Leetcode challenge: Remove K Digits
Code: https://colab.research.google.com/drive/1zwh7pppur0pIoEgi3mNOI3cRV9GBBZ0E?usp=sharing  
Author: Ruizhe Li  
Date: 05/11/2020  

#### Question:
Given a non-negative integer num represented as a string, remove k digits from the number so that the new number is the smallest possible.  

**Note:**
* The length of num is less than 10002 and will be ≥ k.
* The given num does not contain any leading zero.  

**Example 1:** 
```
Input: num = "1432219", k = 3
Output: "1219"
Explanation: Remove the three digits 4, 3, and 2 to form the new number 1219 which is the smallest.
```

**Example 2:**
```
Input: num = "10200", k = 1
Output: "200"
Explanation: Remove the leading 1 and the number is 200. Note that the output must not contain leading zeroes.
```
**Example 3:**
```
Input: num = "10", k = 2
Output: "0"
Explanation: Remove all the digits from the number and it is left with nothing which is 0.
```

#### Solution: Greedy with stack
Copied from the solution:
We use a stack to hold the digits that we would keep at the end.  

Iterating the sequence of digits from left to right, the main loop can be broken down as follows:  

* 1). for each digit, if the digit is less than the top of the stack, i.e. the left neighbor of the digit, then we pop the stack, i.e. removing the left neighbor. At the end, we push the digit to the stack.

* 2). we repeat the above step (1) until any of the conditions does not hold any more, e.g. the stack is empty (no more digits left). or in another case, we have already removed k digits, therefore mission accomplished.

```python
class Solution:
  def removeKdigits(self, num: str, k: int) -> str:
    numStack = []
    
    # Construct a monotone increasing sequence of digits
    for digit in num:
      while k and numStack and numStack[-1] > digit:
        numStack.pop()
        k -= 1

      numStack.append(digit)
    
    # - Trunk the remaining K digits at the end
    # - in the case k==0: return the entire list
    finalStack = numStack[:-k] if k else numStack
    
    # trip the leading zeros
    return "".join(finalStack).lstrip('0') or "0"
```