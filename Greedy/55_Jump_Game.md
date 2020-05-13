# 55. Jump Game

Author: Xiangde Zeng

## Problem
Given an array of non-negative integers, you are initially positioned at the first index of the array.

Each element in the array represents your maximum jump length at that position.

Determine if you are able to reach the last index.

Input:
```
 nums = [2,3,1,1,4]
```
Output:
```
 true
```

Explanation:
```
Jump 1 step from index 0 to 1, then 3 steps to the last index.
```

## Ideas

**First idea:**  
Use dynamic programming.
**How to do:**  
Allocate a boolean dp arrat. dp[i] = true means we can reach index i in a bunch of finite jumps. Starting from dp[0] = true, we use two loops to record each step. Total time complexity: O(n^2)

## Better answer from post

Maintain a variable max to indicate the current index we can reach so far. When iterating the array, note the farthest index it can reach and compare the max variable. If max reaches or exceeds the end of the index, than return true. If max is still behind the tail of the array at the end of the iteration, return false.

```
class Solution {
    public boolean canJump(int[] nums) {
        int max = 0;
        if(max == nums.length - 1) return true;
        for(int i = 0;i<nums.length;i++){
            if(nums[i] == 0){
                if(i == max) return false;
                continue;
            }
            if(nums[i]+i > max) max = nums[i] + i;
            if(max >= nums.length-1) return true;
        }
        return false;
    }
}
```

