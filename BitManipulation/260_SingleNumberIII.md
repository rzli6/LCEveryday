### 260. Single Number III
LC link: https://leetcode.com/problems/single-number-iii/  
Code: https://colab.research.google.com/drive/1zwh7pppur0pIoEgi3mNOI3cRV9GBBZ0E?usp=sharing  
Author: Ruizhe Li  
Date: 05/12/2020

#### Solution:
1. Calculate a bitmask with XOR 
1. Use the last different bit to distinguish the two numbers.  

Takeaway:  
* Use `bitmask & (-bitmask)` to isolate the rightmost 1-bit.

#### Code:
```python
class Solution:
    def singleNumber(self, nums: int) -> List[int]:
        # difference between two numbers (x and y) which were seen only once
        bitmask = 0
        for num in nums:
            bitmask ^= num
        
        # rightmost 1-bit diff between x and y
        diff = bitmask & (-bitmask)
        
        x = 0
        for num in nums:
            # bitmask which will contain only x
            if num & diff:
                x ^= num
        
        return [x, bitmask^x]
```