# 713. Subarray Product Less Than K

2020/05/26 ZTH

### Problem Description

Your are given an array of positive integers `nums`.

Count and print the number of (contiguous) subarrays where the product of all the elements in the subarray is less than `k`.

**Example 1:**

```
Input: nums = [10, 5, 2, 6], k = 100
Output: 8
Explanation: The 8 subarrays that have product less than 100 are: [10], [5], [2], [6], [10, 5], [5, 2], [2, 6], [5, 2, 6].
Note that [10, 5, 2] is not included as the product of 100 is not strictly less than k.
```



**Note:**

`0 < nums.length <= 50000`.

`0 < nums[i] < 1000`.

`0 <= k < 10^6`.



### Algorithm

* key point: sliding window ==> for each right element, we maintain a sliding window with the left boundary be the position of left-most element such that their products is less than k

  ```
  sliding window for position [i, i+1, ..., j]
  i is smallest such that nums[i] * nums[i+1] * ... * nums[j] < k
  ```

* As nums[i] is positive integers, there is no 0 inside, which guarantees that the left-most position for each right element is increasing when we move right

  ```
  left-most position for right 0 (1st) <= left-most position for right 1 (2nd) <= .... <= left-most position for right len(nums)-1 (last element)
  ```

* Keep a product value for the sliding window:

  * when we move one element right, multiply product value with current one

    ```
    product *= nums[right] # right increases from 0 to len(nums)-1
    ```

  * check whether current product value is less than k, if not, move the left boundary until satisfy the condition

    ```
    while product >= k:
    	product /= nums[left] # left: current sliding window left boundary
    	left += 1 # when nums[right] >= k, we would get final left = right + 1, product = 1
    ```

* For each right element, # of subarray satisfy the condition

  ```
  = right - left + 1 = # elements in the sliding window 
  ```

  * as subarray must be continuous, we could only have the following situations

    ```
    e.g. assume 1,2,3,4 is the sliding window
    		 4; 3,4; 2,3,4; 1,2,3,4
    ```

* Complexity Analysis

  * Time: O(N)

  * Space: O(1)

    

### Code

```python
class Solution:
    def numSubarrayProductLessThanK(self, nums: List[int], k: int) -> int:
        if k <= 1: return 0
        ans, product, left = 0, 1, 0
        
        for right, value in enumerate(nums):
            product *= value
            while product >= k:
                product /= nums[left]
                left += 1
            ans += right - left + 1
        return ans
```

