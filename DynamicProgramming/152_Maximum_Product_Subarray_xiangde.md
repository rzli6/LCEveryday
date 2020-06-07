# 152. Maximum Product Subarray

2020/06/06 Xiangde Zeng

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



### 1. Dynamic programming (max and min dp)
Use two array max[i] and min[i] to refer the maximum and minimum product of subarray ending at index i


### Code

```Java
class Solution {
    public int maxProduct(int[] nums) {
        int n = nums.length;
        int[] max = new int[n];
        int[] min = new int[n];
        max[0] = nums[0];
        min[0] = nums[0];
        int res = nums[0];
        for(int i = 1;i < n;i++){
            int first = max[i-1] * nums[i];
            int second = min[i-1] * nums[i];
            if(nums[i] > 0){
                max[i] = Math.max(nums[i],first);
                min[i] = Math.min(nums[i],second);
            }
            else{
                max[i] = Math.max(nums[i],second);
                min[i] = Math.min(nums[i],first);
            }
            res = Math.max(res,max[i]);
        }
        return res;
        
    }
}
            
```

### 2. Dynamic programming with constant space
We do not need an array here, two variabls to record the corrent max and min is ok


### Code

```Java
class Solution {
    public int maxProduct(int[] nums) {
        int n = nums.length;
        int max = nums[0];
        int min = nums[0];
        int res = nums[0];
        for(int i = 1;i < n;i++){
            int first = max * nums[i];
            int second = min * nums[i];
            if(nums[i] > 0){
                max = Math.max(nums[i],first);
                min = Math.min(nums[i],second);
            }
            else{
                max = Math.max(nums[i],second);
                min = Math.min(nums[i],first);
            }
            
            res = Math.max(res,max);
        }
        return res;
        
    }
}
            
```