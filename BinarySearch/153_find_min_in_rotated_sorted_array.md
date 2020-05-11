### 153. Find Minimum in Rotated Sorted Array
LC link: https://leetcode.com/problems/find-minimum-in-rotated-sorted-array/  
Code: https://colab.research.google.com/drive/1zwh7pppur0pIoEgi3mNOI3cRV9GBBZ0E?usp=sharing  
Author: Ruizhe Li  
Date: 05/10/2020

#### Solution:  
As the list can be divided into two halves of sorted arrays. We can use binary search to find the "break" point, where left is larger than right.  

#### Code:
```python
class Solution:
  def findMin(self, nums: List[int]) -> int:
    l, r = 0, len(nums) # answer in the interval [l,r)
    while l < r:
      mid = (l+r)//2
      if nums[mid] >= nums[0]:
        # break point on the right
        l = mid+1
      else: # break point on the left or right on it
        r = mid
    return nums[l] if l < len(nums) else nums[0]
```