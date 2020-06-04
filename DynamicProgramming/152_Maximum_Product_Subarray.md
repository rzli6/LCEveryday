# 152. Maximum Product Subarray

2020/06/04 ZTH

### Problem Description

Given an integer array `nums`, find the contiguous subarray within an array (containing at least one number) which has the largest product.

**Example 1:**

```
Input: [2,3,-2,4]
Output: 6
Explanation: [2,3] has the largest product 6.
```

**Example 2:**

```
Input: [-2,0,-1]
Output: 0
Explanation: The result cannot be 2, because [-2,-1] is not a subarray.
```



### Algorithm

* Use maxarray and minarray to store the max and min subarrary product up to each position

  ```
  maxarray[i]: maximum subarray product with end position at i
  minarray[i]: minimum subarray product with end position at i
  ```

* We use number from previous position to compute current position

  * Only three cases to compute max and min subarray product

  ```
  maxarray[i] = max(maxarray[i]*nums[i], minarray[i]*nums[i], nums[i])
  minarray[i] = min(maxarray[i]*nums[i], minarray[i]*nums[i], nums[i])
  ```

* Complexity Analysis

  * Time: O(n)
  * Space: O(n)



### Code

```python
class Solution:
    def maxProduct(self, nums: List[int]) -> int:
        if not nums: return 0
        maxarray, minarray, ans = [nums[0]], [nums[0]], nums[0]
        for i in range(1, len(nums)):
            current = max(maxarray[i-1] * nums[i], minarray[i-1] * nums[i], nums[i])
            ans = max(ans, current)
            maxarray.append(current)
            minarray.append(min(maxarray[i-1] * nums[i], minarray[i-1] * nums[i], nums[i]))
        return ans
            
```

