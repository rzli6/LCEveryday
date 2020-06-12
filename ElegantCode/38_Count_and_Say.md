# 38. Count and Say

Author: LIU Zhuofei  
Date: 2020.6.10  
Rating: 3.0/5.0

## Problem
The count-and-say sequence is the sequence of integers with the first five terms as following:
```
1.     1
2.     11
3.     21
4.     1211
5.     111221
1 is read off as "one 1" or 11.
11 is read off as "two 1s" or 21.
21 is read off as "one 2, then one 1" or 1211.
```
Given an integer n where 1 ≤ n ≤ 30, generate the nth term of the count-and-say sequence. You can do so recursively, in other words from the previous member read off the digits, counting the number of digits in groups of the same digit.

Note: Each term of the sequence of integers will be represented as a string.

 

Example:
```
Input: 1
Output: "1"
Explanation: This is the base case.

Input: 4
Output: "1211"
Explanation: For n = 3 the term was "21" in which we have two groups "2" and "1", "2" can be read as "12" which means frequency = 1 and value = 2, the same way "1" is read as "11", so the answer is the concatenation of "12" and "11" which is "1211".
```

## Elegant code
[Source](https://leetcode.com/problems/count-and-say/discuss/15999/4-5-lines-Python-solutions)

Normal code:  
```python
class Solution:
    def countAndSay(self, n):
        """
        :type n: int
        :rtype: str
        """
        def cns(str_):
            res = ''
            str_ += '#'
            c = 1
            for i in range(len(str_) - 1):
                if str_[i] == str_[i+1]:
                    c += 1
                    continue
                else:
                    res += str(c) + str_[i]
                    c = 1
            
            return res
            
        start = '1'
        for i in range(n-1):
            start = cns(start)
        return start
```

elegant code 1:using a regular expression
```python
def countAndSay(self, n):
    s = '1'
    for _ in range(n - 1):
        s = re.sub(r'(.)\1*', lambda m: str(len(m.group(0))) + m.group(1), s)
    return s
```

elegant code 2:using a regular expression
```python
def countAndSay(self, n):
    s = '1'
    for _ in range(n - 1):
        s = ''.join(str(len(group)) + digit
                    for group, digit in re.findall(r'((.)\2*)', s))
    return s
```

elegant code 3:using groupby
```python
def countAndSay(self, n):
    s = '1'
    for _ in range(n - 1):
        s = ''.join(str(len(list(group))) + digit
                    for digit, group in itertools.groupby(s))
    return s
```