# 43. Multiply Strings

Author: zhuofei  
Date: 6.14  

## Problem  
Given two non-negative integers num1 and num2 represented as strings, return the product of num1 and num2, also represented as a string.
```
Input: num1 = "123", num2 = "456"
Output: "56088"
```
Note:
1. The length of both num1 and num2 is < 110.
2. Both num1 and num2 contain only digits 0-9.
3. Both num1 and num2 do not contain any leading zero, except the number 0 itself.
4. You must not use any built-in BigInteger library or convert the inputs to integer directly.

## Elegant Code
```python
def multiply(self, num1, num2):
    res = [0]* (len(num1) + len(num2))
     for i, e1 in enumerate(reversed(num1)):
         for j, e2 in enumerate(reversed(num2)):
             res[i+j] += int(e1) * int(e2)
             res[i+j+1] += res[i+j]/10
             res[i+j] %= 10
 
     while len(res) > 1 and res[-1] == 0: res.pop()
     return ''.join( map(str,res[::-1]) )
```
