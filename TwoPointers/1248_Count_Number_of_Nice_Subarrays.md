# 1248. Count Number of Nice Subarrays

2020/06/17 ZTH

### Problem Description

Given an array of integers `nums` and an integer `k`. A subarray is called **nice** if there are `k` odd numbers on it.

Return the number of **nice** sub-arrays.

 

**Example 1:**

```
Input: nums = [1,1,2,1,1], k = 3
Output: 2
Explanation: The only sub-arrays with 3 odd numbers are [1,1,2,1] and [1,2,1,1].
```

**Example 2:**

```
Input: nums = [2,4,6], k = 1
Output: 0
Explanation: There is no odd numbers in the array.
```

**Example 3:**

```
Input: nums = [2,2,2,1,2,2,1,2,2,2], k = 2
Output: 16
```

 

**Constraints:**

- `1 <= nums.length <= 50000`
- `1 <= nums[i] <= 10^5`
- `1 <= k <= nums.length`



### Algorithm

* To get subarray with k odd numbers, we could replace all even numbers by 0 and all odd numbers by 1 and find subarray whose sum equals k

* We record the prefix sum to each position of the input list, and once we could find two sums that differ by k, we get the required subarray

  * ```
    e.g.        1 0 0 1 1 1 0 0 1
    prefix sum  1 1 1 2 3 4 4 4 5
    k = 2:      (3,1); (4,2); (5,3)
    ```

  * Thus, we could use a dictionary to count the number of each prefix sum. For each sum value m, we check whether m-k in the dictionary, if yes, add dic[m-k] to the answer and update dic[m]

* Complexity Analysis

  * Time: O(N)
  * Space: O(N)



### Code

```python
class Solution:
    def numberOfSubarrays(self, nums: List[int], k: int) -> int:
        nums[0] = nums[0] % 2
        for i in range(1,len(nums)):
            nums[i] = nums[i-1] + nums[i] % 2
        dic, ans = {0:1}, 0
        for e in nums:
            if e - k in dic: ans += dic[e-k]
            if e not in dic: dic[e] = 1
            else: dic[e] += 1
        return ans
        
```

