# 45. Jump Game II

Author: Xiangde Zeng

## Problem
Given an array of non-negative integers, you are initially positioned at the first index of the array.

Each element in the array represents your maximum jump length at that position.

Your goal is to reach the last index in the minimum number of jumps.

Input:
```
 nums = [2,3,1,1,4]
```
Output:
```
 2
```

Explanation:
```
The minimum number of jumps to reach the last index is 2.
Jump 1 step from index 0 to 1, then 3 steps to the last index.
```

## Ideas

**First idea:**  
Use dynamic programming.
**How to do:**  
Allocate a int dp arrat. dp[i] refers to the minimum step we need to jump to reach index i. Initially, dp[0] = 0; During the iteration, update the dp[i] based on the maximum step it can jump. After the iteration, dp[n-1] would be the result we needed. Time complexity: O(n^2). Space complexity: O(n)

## Better answer from post

Greedy: Analysis: Use two pointers, pre and cur, to record the farthest step the pointer can reach so far. Initially pre = cur = 0; When cur does not reach the end, try to find the logest jump it can reach starting from pre to cur. Update cur to the farthest index. Iterate it until we reach to the end.

```
class Solution {
    public int jump(int[] nums) {
        int n = nums.length;
        int res = 0;
        int pre = 0;
        int cur = 0;
        int i = 0;
        while(cur < n - 1){
            res++;
            pre = cur;
            while(i <= pre){
                cur = Math.max(cur,i+nums[i]);
                i++;
            }
            if(pre == cur) return -1;
        }
        return res;
    }
}
```

