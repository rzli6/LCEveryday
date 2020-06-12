# 1208. Get Equal Substrings Within Budget

2020/06/12 ZLY

### Problem Description

You are given two strings `s` and `t` of the same length. You want to change `s` to `t`. Changing the `i`-th character of `s` to `i`-th character of `t` costs `|s[i] - t[i]|` that is, the absolute difference between the ASCII values of the characters.

You are also given an integer `maxCost`.

Return the maximum length of a substring of `s` that can be changed to be the same as the corresponding substring of `t`with a cost less than or equal to `maxCost`.

If there is no substring from `s` that can be changed to its corresponding substring from `t`, return `0`.



### Algorithm

Basic idea is sliding window. We just keep modifying the start and end points of the window to satisfy the condition (`totalCost < maxCost`) and find the longest length among these windows.



### Code

```python
def equalSubstring(self, s: str, t: str, maxCost: int) -> int:
    def difference(a,b):
        return abs(ord(a)-ord(b))
    cost = 0
    start = 0
    result = 0
    for i in range(len(s)):
        cost += difference(s[i],t[i])
        if cost<=maxCost:
            result = max(result,i-start+1)
        else:
            while cost>maxCost:
                cost -= difference(s[start],t[start])
                start += 1
    result = max(result,i-start+1)
    return result
```