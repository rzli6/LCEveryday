### [231. Power of Two](https://leetcode.com/problems/power-of-two/)
Author: Ruizhe Li  
Date: 06/08/2020

#### Solution:
Key Point: then n & (n-1) is 0 iff n is a power of two or n is 0.

#### Code:
```python
class Solution:
  def isPowerOfTwo(self, n: int) -> bool:
    if n == 0:
      return False
    
    return n & (n-1) == 0
```