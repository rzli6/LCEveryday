### 438. Find All Anagrams in a String
LC link: https://leetcode.com/problems/find-all-anagrams-in-a-string/  
Code: https://colab.research.google.com/drive/1zwh7pppur0pIoEgi3mNOI3cRV9GBBZ0E?usp=sharing  
Author: Ruizhe Li  
Date: 05/26/2020

#### Solution:
Sliding window:
* Form a window of size *len(p)*
* Count the word frequencies in the window
* Compare the word frequency counting with word frequency of *p*
  * Append if frequencies are same
  * Ignore otherwise
* Slide one step to the right and repeat the previous steps until reach the end of string *s*

#### Solution:
```python
class Solution:
  def findAnagrams(self, s: str, p: str) -> List[int]:
    # if the length of s is less than p
    # there must be no anagram of p in s
    if len(s) < len(p):
      return []
    
    # initialize the window counters of size len(p)
    cntP, cntS = [0]*26, [0]*26

    # convert string to list of integers
    p = [ord(c)-ord('a') for c in p]
    s = [ord(c)-ord('a') for c in s]

    # initialize the first window
    for pp, ss in zip(p, s):
      cntP[pp] += 1
      cntS[ss] += 1
    
    # store the results in res
    res = [0] if cntP == cntS else []

    # sliding window
    for i in range(1, len(s)-len(p)+1):
      cntS[s[i-1]] -= 1
      cntS[s[i+len(p)-1]] += 1
      if cntP == cntS:
        res.append(i)
    
    return res      
```