# 567. Permutation in String

2020/05/25 ZTH

### Problem Description

Given two strings **s1** and **s2**, write a function to return true if **s2** contains the permutation of **s1**. In other words, one of the first string's permutations is the **substring** of the second string.

 

**Example 1:**

```
Input: s1 = "ab" s2 = "eidbaooo"
Output: True
Explanation: s2 contains one permutation of s1 ("ba").
```

**Example 2:**

```
Input:s1= "ab" s2 = "eidboaoo"
Output: False
```

 

**Constraints:**

- The input strings only contain lower case letters.
- The length of both given strings is in range [1, 10,000].



### Algorithm

* key point ==> sliding window

* keep a sliding window with size s1 for the elements in s2, compare the element of s2 with s1

* way 1 each time compute a new counter (dictionary) for the s1 length element of s2, and match the counter with s1 see whether the same

  * if same: return True
  * if not: move sliding window one element later and continue

  ```
  time complexity O(l1 * (l2-l1))
  space complexity O(l1)
  ```

* way 2 each time we remove the first element of the counter out and add the newest element into the counter and compare with s1

  * if same: return True
  * if not: move sliding window one element later and continue 

  ```
  time complexity O(l1 + l2)
  space complexity O(l1)
  ```

  

### Code

```python
class Solution:
    def checkInclusion(self, s1: str, s2: str) -> bool:
        # way1 sliding window ==> O(l1*(l2-l1)) time, O(l1) space
        if len(s1) > len(s2): return False
        base = collections.Counter(s1)
        for i in range(len(s2)-len(s1)+1):
            current = collections.Counter(s2[i:i+len(s1)])
            if current == base: return True
        return False
```

```python
class Solution:
    def checkInclusion(self, s1: str, s2: str) -> bool:
        # way2 sliding window ==> O(l1 + l2) time, O(l1) space
        if len(s1) > len(s2): return False
        base, current = collections.Counter(s1), collections.Counter(s2[:len(s1)])
        if base == current: return True
        for i in range(len(s1),len(s2)):
            if current[s2[i-len(s1)]] == 1: del current[s2[i-len(s1)]] 
            else: current[s2[i-len(s1)]] -= 1
            if s2[i] not in current: current[s2[i]] = 1
            else: current[s2[i]] += 1
            if current == base: return True
        return False
```

