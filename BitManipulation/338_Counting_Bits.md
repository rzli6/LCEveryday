### 338. Counting Bits
LC link: https://leetcode.com/problems/counting-bits/
Code: https://colab.research.google.com/drive/1zwh7pppur0pIoEgi3mNOI3cRV9GBBZ0E?usp=sharing  
Author: Ruizhe Li  
Date: 05/29/2020

#### Solution:
**Dynamic Programming**  
For each number cur:
* Find a smaller number with one less 1, `cur&(cur-1)` *set rightmost 1 to 0*
* Add one to res[cur&(cur-1)]

#### Code:
```python
class Solution:
  def countBits(self, num: int) -> List[int]:
    res = [0]*(num+1)
    for i in range(1, num+1):
      res[i] = res[i&(i-1)]+1
    return res
```