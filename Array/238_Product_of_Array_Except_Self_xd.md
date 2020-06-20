# 238. Product of Array Except Self

2020/06/18 XDDD

### Problem Description

Given an array `nums` of *n* integers where *n* > 1,  return an array `output` such that `output[i]` is equal to the product of all the elements of `nums` except `nums[i]`.

e.g.

```
Input:  [1,2,3,4]
Output: [24,12,8,6]
```

### Algorithms

* Way 1: Two arrays

  We use two arrays to multiply the array: one starting from left to right and another starting from right to left. Then combine these two arrays together to get the result

* Way 2: One array

  We can shrink one array, say the right-to-left array, into one variable to save the space. 



### Codes

```java
//Way 1
class Solution {
    public int[] productExceptSelf(int[] nums) {
        int n = nums.length;
        if(n <= 1) return nums;
        int[] left = new int[n];
        int[] right = new int[n];
        left[0] = 1;
        right[n-1] = 1;
        for(int i = 1;i<n;i++){
            left[i] = nums[i-1] * left[i-1];
        }
        for(int i = n-2; i >= 0;i--){
            right[i] = nums[i+1] * right[i+1];
        }
        for(int i = 0;i<n;i++){
            left[i] *= right[i];
        }
        return left;
    }
}
```

```java
class Solution {
    public int[] productExceptSelf(int[] nums) {
        int n = nums.length;
        if(n <= 1) return nums;
        int[] ans = new int[n];
        ans[0] = 1;
        for(int i = 1;i<n;i++){
            ans[i] = nums[i-1] * ans[i-1];
        }
        int R = 1;
        for(int i = n-1; i >= 0;i--){
            ans[i] *= R;
            R *= nums[i];
        }
        return ans;
    }
}
```

