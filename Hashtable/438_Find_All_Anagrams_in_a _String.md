# 438. Find All Anagrams in a String

2020/05/29 ZTH

### Problem Description

Given a string **s** and a **non-empty** string **p**, find all the start indices of **p**'s anagrams in **s**.

Strings consists of lowercase English letters only and the length of both strings **s** and **p** will not be larger than 20,100.

The order of output does not matter.

**Example 1:**

```
Input:
s: "cbaebabacd" p: "abc"

Output:
[0, 6]

Explanation:
The substring with start index = 0 is "cba", which is an anagram of "abc".
The substring with start index = 6 is "bac", which is an anagram of "abc".
```



**Example 2:**

```
Input:
s: "abab" p: "ab"

Output:
[0, 1, 2]

Explanation:
The substring with start index = 0 is "ab", which is an anagram of "ab".
The substring with start index = 1 is "ba", which is an anagram of "ab".
The substring with start index = 2 is "ab", which is an anagram of "ab".
```



### Algorithm

* keep a dictionary to record the occurrence of each character in p
* for each length-p substring of s, count the occurrence of each character and check whether the same with p, if yes, add the starting position to answer
* Two ways of substring matching:
  * Way1: each time extract a length-p substring in s
  * Way2: move like a sliding window, current is based on previous one by removing the first and adding the last
* Complexity Analysis
  * Way1: O(s*p) time, O(p) space
  * Way2: O(s) time, O(p) space



### Code

```python
class Solution:
    def findAnagrams(self, s: str, p: str) -> List[int]:
        # way 1: O(s*p) time, O(p) space
        base, ans = collections.Counter(p), []
        for i in range(len(s)-len(p)+1):
            if collections.Counter(s[i:i+len(p)]) == base:
                ans.append(i)
        return ans
```

```python
class Solution:
    def findAnagrams(self, s: str, p: str) -> List[int]:
        # way 2: O(s) time, O(p) space
        base, ans = collections.Counter(p), []
        for i in range(len(s)-len(p)+1):
            if i == 0: current = collections.Counter(s[i:i+len(p)])
            else: 
                current[s[i-1]] -= 1
                if current[s[i-1]] == 0: del current[s[i-1]]
                if s[i+len(p)-1] not in current: current[s[i+len(p)-1]] = 1
                else: current[s[i+len(p)-1]] += 1
            if current == base: ans.append(i)
        return ans
```

