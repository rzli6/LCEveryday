### [438. Find All Anagrams in a String](https://leetcode.com/problems/reorganize-string/)
Author: Ruizhe Li  
Date: 06/02/2020


#### Solution:
We provide 2 solutions:
1. Elegant Python solution which needs only 4 lines of codes.  
Idea:  
    1. Sort the string according to char frequency. 
    1. Put most common chars at odd positions and least common chars at even positions.
1. O(N) efficient solution:
    1. Get char frequencies.
    1. Put the most frequent char in 2,4,6,8,..
    1. Put other char in the empty postions.

```python
from collections import Counter

class Solution:
  def reorganizeString1(self, S: str) -> str:
    a = sorted(sorted(S), key = S.count) # sort according to char frequency
    h = len(a) // 2
    a[1::2], a[::2] = a[:h], a[h:] # put elements to odd and even positions
    return ''.join(a) * (a[-1:] != a[-2:-1]) # check the last 2 indexes
  def reorganizeString2(self, S: str) -> str:
    max_char = max([a for a in ctr], key = lambda a: ctr[a])
    if ctr[max_char] > (len(s)+1)/2:
      return ''
    res = list(''.join([a*ctr[a] for a in ctr if a != max_char]+[max_char*ctr[max_char]]))
    mid = len(res)//2
    res[1::2], res[::2] = res[:mid], res[mid:]
    return ''.join(res)
```