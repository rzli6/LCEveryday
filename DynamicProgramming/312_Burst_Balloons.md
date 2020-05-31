### 312. Burst Balloons
LC link: https://leetcode.com/problems/burst-balloons/  
Code: https://colab.research.google.com/drive/1zwh7pppur0pIoEgi3mNOI3cRV9GBBZ0E?usp=sharing  
Author: Ruizhe Li  
Date: 05/31/2020

#### Solution:
This is an amazing DP problem. In short you need to think reversly!  
Instead of thinking of which balloon to burst first, we'd better think which balloon is best to be bursted lastly. Because the value of the last bursted balloon is determinated.  
For example, nums=[3,1,5,8]
* Add 1 to beginning and ending of the nums,
nums=[1,3,1,5,8]
* Try which is best to be lastly bursted
* Recursively solve left and right subproblems.

#### Code:
```python
from functools import lru_cache

class Solution:
  def maxCoins(self, nums: List[int]) -> int:
    nums = [1] + nums + [1]
    
    @lru_cache(None) # Wrapper to cache the result of the dp function
    def dp(left, right):
      if left+1 == right: # if there are less than 2 elements, return 0
        return 0
      # Try each one of the element to be lastly bursted
      # return the maximum value of all possbilities
      return max(nums[left]*nums[i]*nums[right]+dp(left,i)+dp(i,right) for i in range(left+1, right))
    
    return dp(0, len(nums)-1)
```            
