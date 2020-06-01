# 763. Partition Labels

2020/06/01 ZTH

### Problem Description

A string `S` of lowercase letters is given. We want to partition this string into as many parts as possible so that each letter appears in at most one part, and return a list of integers representing the size of these parts.



**Example 1:**

```
Input: S = "ababcbacadefegdehijhklij"
Output: [9,7,8]
Explanation:
The partition is "ababcbaca", "defegde", "hijhklij".
This is a partition so that each letter appears in at most one part.
A partition like "ababcbacadefegde", "hijhklij" is incorrect, because it splits S into less parts.
```



**Note:**

1. `S` will have length in range `[1, 500]`.
2. `S` will consist of lowercase letters (`'a'` to `'z'`) only.



### Algorithm

* For each character, at least a part [start, end] is needed to keep all this character within this gourp

  ```
  e.g.   'ababacbabc'
  index= '0123456789'
  for 'a': [0,7] is needed
  ```

* But for a pariticular part we selected, we need to pay attention to other characters appearing within this part

  ```
  e.g.   'ababacbabc'
  index= '0123456789'
  for 'a': [0,7] is needed
  we select [0,7], but within [0,7], we have 'b', 'c'
  if we split at 7, 'b', 'c' not satisfy the requirement
  ```

* Thus, we need to update end position by processing all characters' last occurrence position within the group

  ```
  e.g.   'ababacbabc'
  index= '0123456789'
  for 'a': [0,7] is needed
  for 'b': end position = 8
  for 'c': end position = 9
  update 'b': [0,8]
  update 'c': [0,9]
  ```

* We start from 1st character and update the end position, once we finish the first part, append the length to answer and start from end + 1 position continuing the same process

* Thus, we just need to keep the last occurrence position of each character, with start from 0

* Complexity Analysis

  * Time: O(N) N = len(S)
  * Space: O(1), at most 26 characters



### Code

```python
class Solution:
    def partitionLabels(self, S: str) -> List[int]:
        # O(N) time, O(1) space
        dic, ans = {value: key for key, value in enumerate(S)}, []
        start, end = 0, 0
        for key, value in enumerate(S):
            end = max(end, dic[S[key]])
            if key == end:
                ans.append(end-start+1)
                start = end + 1
        return ans
                
        
        
            
        
```

