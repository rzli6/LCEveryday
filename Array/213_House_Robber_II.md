# 213. House Robber II

2020/05/22 ZTH

### Problem Description

You are a professional robber planning to rob houses along a street. Each house has a certain amount of money stashed. All houses at this place are **arranged in a circle.** That means the first house is the neighbor of the last one. Meanwhile, adjacent houses have security system connected and **it will automatically contact the police if two adjacent houses were broken into on the same night**.

Given a list of non-negative integers representing the amount of money of each house, determine the maximum amount of money you can rob tonight **without alerting the police**.

**Example 1:**

```
Input: [2,3,2]
Output: 3
Explanation: You cannot rob house 1 (money = 2) and then rob house 3 (money = 2),
             because they are adjacent houses.
```

**Example 2:**

```
Input: [1,2,3,1]
Output: 4
Explanation: Rob house 1 (money = 1) and then rob house 3 (money = 3).
             Total amount you can rob = 1 + 3 = 4.
```



### Algorithm

* allocate a dp variable with length n to store the maximum amount of money up to that position

  * 1st element

    ```
    dp[0] = nums[0], simply the 1st element
    ```

  * 2nd element

    ```
    dp[1] = max(nums[0], nums[1]), maximum value among 1st and 2nd elements
    ```

  * other elements

    ```
    dp[i] = max(dp[i-2] + nums[i], dp[i-1])
    ```

    

* circle situation

  * do the above process from 1st position to the second last position
  * do the above process from 2nd position to the last position

* Complexity analysis:

  * O(n) time, 2 scans
  * O(n) space, one additional variable list - dp



### Code

```python
class Solution:
    def rob(self, nums: List[int]) -> int:
        if not nums: return 0
        if len(nums) == 1: return nums[0]
        if len(nums) == 2: return max(nums[0],nums[1])
        # O(n) time, O(n) space
        dp = [0 for i in range(len(nums))]
        dp[0], dp[1] = nums[0], max(nums[0],nums[1])
        ans = max([0, dp[0], dp[1]])
        for i in range(2, len(nums)-1):
            dp[i] = max(dp[i-2] + nums[i], dp[i-1])
            ans = max(ans, dp[i])
        dp = [0 for i in range(len(nums))]
        dp[1], dp[2] = nums[1], max(nums[1],nums[2])
        for i in range(3, len(nums)):
            dp[i] = max(dp[i-2] + nums[i], dp[i-1])
            ans = max(ans, dp[i])
        nums[2] = max(nums[1],nums[2])
        # for i in range(3, len(nums)):
        #     nums[i] = max(nums[i-2] + nums[i], nums[i-1])
        #     ans = max(ans, nums[i])
        return ans
        
```

