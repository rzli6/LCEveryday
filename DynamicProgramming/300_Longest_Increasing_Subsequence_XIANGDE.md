# 300. Longest Increasing Subsequence

2020/06/02 Xiangde Zeng

### Problem Description

Given an unsorted array of integers, find the length of longest increasing subsequence.

**Example:**

```
Input: [10,9,2,5,3,7,101,18]
Output: 4 
Explanation: The longest increasing subsequence is [2,3,7,101], therefore the length is 4. 
```

**Note:**

- There may be more than one LIS combination, it is only necessary for you to return the length.
- Your algorithm should run in O(*n2*) complexity.

**Follow up:** Could you improve it to O(*n* log *n*) time complexity?



### Algorithm 1

1. Dynamic Programming: mark dp[i] as the longest subsequnece ends with i. Tracking each possible situation using two nested loop. Overall time complexity: O(n^2)



```Java
class Solution {
    public int lengthOfLIS(int[] nums) {
        int n = nums.length;
        if(n == 0) return 0;
        int[] dp = new int[n];
        dp[0] = 1;
        int global_max = 1;
        for(int i = 1;i<n;i++){
            int max = 0;
            for(int j = 0;j<i;j++){
                if(nums[j] < nums[i] && max < dp[j]) max = dp[j];
            }
            dp[i] = max + 1;
            global_max = Math.max(global_max,dp[i]);
        }
        return global_max;
    }
}

```

2. We can speedup the search by using the binary search

```Java
class Solution {
    public int lengthOfLIS(int[] nums) {
        int n = nums.length;
        int[] dp = new int[n];
        int len = 0;
        for(int x:nums){
            int i = Arrays.binarySearch(dp,0,len,x);
            if(i<0) i = -(i+1);
            dp[i] = x;
            if(len == i) len++;
        }
        return len;
    }
    
    
}
```