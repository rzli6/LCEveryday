### 159. Longest Substring with At Most Two Distinct Characters
LC link: https://leetcode.com/problems/longest-substring-with-at-most-two-distinct-characters/  
Code: https://colab.research.google.com/drive/1zwh7pppur0pIoEgi3mNOI3cRV9GBBZ0E?usp=sharing  
Author: Ruizhe Li  
Date: 05/11/2020

#### Solution:
This is a standard sliding window (two pointers) question. We maintain the left and right boundary of the window, in which the substring has at most two distinct characters.  
* If the substring contains at least 2 distinct characters, we move the left boundary to the right.
* If the substring contains at most 2 distinct characters, we move the right boundary to the right and update the max length of the substring.

#### Code:
```python
from collections import defaultdict
class Solution:
  def lenghtOfLongestSubstringTwoDistinct(self, s: str)->int:
    n = len(s)
    if n < 3:
      # trivial case when the string contains at most 2 characters
      return n
    l, r = 0, 0
    pos = defaultdict(int) # position of the right most position of each char
    max_len = 2
    
    while r < n:
      if len(pos) < 3:
        pos[s[r]] = r
        r += 1
      if len(pos) == 3:
        del_idx = min(pos.values())
        del pos[s[del_idx]]
        l = del_idx + 1
      max_len = max(max_len, r-l)
    return max_len
```