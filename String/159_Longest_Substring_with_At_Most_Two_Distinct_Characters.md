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
from typing import List  

class Solution:
  def singleNumber_sum(self, nums: List[int]) -> int:
    return int((3*sum(set(nums))-sum(nums))/2)

  # k=3, p=1
  def singleNumber_bit(self, nums: List[int]) -> int:
    # for ceiling(log_2 3) =  2
    # initialize 2 counters x1, x2. 
    x1, x2 = 0, 0
    for a in nums:
      x2 ^= x1 & a
      x1 ^= a
      mask = ~(x1 & x2) # for binary representation of 3 is 11
      x1 &= mask
      x2 &= mask
    return x1|x2
  
  def singleNumber_sol(self, nums: List[int]) -> int:
    seen_once = 0 # the number that appears once
    seen_twice = 0 # the number that appers three times
    for num in nums:
      seen_once = ~seen_twice & (seen_once ^ num)
      seen_twice = ~seen_once & (seen_twice ^ num)
    return seen_once
```