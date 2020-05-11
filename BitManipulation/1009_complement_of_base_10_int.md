### 1009. Complement of Base 10 Integer
LC link: https://leetcode.com/problems/single-number-ii/  
Code: https://colab.research.google.com/drive/1zwh7pppur0pIoEgi3mNOI3cRV9GBBZ0E?usp=sharing  
Author: Ruizhe Li  
Date: 05/11/2020

#### Solution:
The key point is how to come up with a correct bit mask. Here we are going to use **highestOneBit OpenJDK algorithm from Hacker's Delight**.  
E.g. N = 100001 is a 2-based integer  
The bitmask is constructed as 100001 -> 110001 -> 111101 -> 111111.
#### Code:
```python
class Solution:
  def bitwiseComplement(self, N: int) -> int:
    if N == 0:
      return 1

    # bitmask has the same length as N and contains only ones 1...1
    bitmask = N
    bitmask |= (bitmask >> 1)
    bitmask |= (bitmask >> 2)
    bitmask |= (bitmask >> 4)
    bitmask |= (bitmask >> 8)
    bitmask |= (bitmask >> 16)

    # flip all bits
    return bitmask ^ N
```