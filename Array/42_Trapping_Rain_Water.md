# 42. Trapping Rain Water

Author: LIU Zhuofei  
Date: 6.13  
Rating: 4.5/5.0

## Problem

Given n non-negative integers representing an elevation map where the width of each bar is 1, compute how much water it is able to trap after raining.

![Example](https://assets.leetcode.com/uploads/2018/10/22/rainwatertrap.png)

```
Input: [0,1,0,2,1,0,1,3,2,1,2,1]
Output: 6
```

## Solution

There are 4 or 5 solutions to solve this problem including stack, double pointer, dynamic programming.

I like solution which uses double pointer most.  

Time complexity: O(n). Single iteration of O(n).  
Space complexity: O(1)O extra space.  

Idea is shown in details in offical solution. Better to see it again.

[Offical Solution](https://leetcode.com/problems/trapping-rain-water/solution/)

```cpp
int trap(vector<int>& height)
{
    int left = 0, right = height.size() - 1;
    int ans = 0;
    int left_max = 0, right_max = 0;
    while (left < right) {
        if (height[left] < height[right]) {
            height[left] >= left_max ? (left_max = height[left]) : ans += (left_max - height[left]);
            ++left;
        }
        else {
            height[right] >= right_max ? (right_max = height[right]) : ans += (right_max - height[right]);
            --right;
        }
    }
    return ans;
}
```