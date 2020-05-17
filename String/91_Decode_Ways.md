# 91. Decode Ways

2020/05/13 ZLY

### Problem Description

A message containing letters from `A-Z` is being encoded to numbers using the following mapping:

```
'A' -> 1
'B' -> 2
...
'Z' -> 26
```

Given a **non-empty** string containing only digits, determine the total number of ways to decode it.

### Algorithm

We use dynamic programming. For each digit in the string s, it can either be independently decoded as a letter (if it is not 0) or be combined with the previous digit (if the combination is between 10 and 26, inclusive). Therefore ,the basic dynamic programming is as follows.

```python
result[0] = 1
# Independent
if s[i]!='0':
    result[i]=result[i-1]
# Combined
if '09'<s[i-1:i+1]<'27':
    if i>1:
        result[i]+=result[i-2]
    else:
        result[i]+=1
```

For example, for string `"abba"`, when we set the end position to be the second `b` (index 2), by looking at the dictionary, we can see that last occurence of `'b'` is at index 1. Therefore, we set the start position to be `1+1=2`, now the length is `2-2+1=0`. Next we set the end position to be the last character `'a'` (index 3). The dictionary tells the last occurence of `'a'` is at index 0. Then this time, the start position should be the larger one between `0+1=1` and the previous start position `2`. Therefore, now the start position is still `2`.

##### *Special case: When the string is start with '0', we can directly return 0.

```python
if s[0]=='0':
    return 0
```