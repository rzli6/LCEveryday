# 42. Trapping Rain Water

2020/05/15 Xander

### Problem Description

Given *n* non-negative integers representing an elevation map where the width of each bar is 1, compute how much water it is able to trap after raining.

link: https://leetcode.com/problems/trapping-rain-water/



e.g.

```
Input: [0,1,0,2,1,0,1,3,2,1,2,1]
Output: 6
```



### Algorithm 

* Two pointer: Generate two pointers l_max and r_max to record the current maximum heights starting from left and starting from right. Move the pointers and check whether the current position is below the maximum height; if so, calculate the difference and add it to the answer. 

  

### Code

```java
class Solution {
    public int trap(int[] height) {
        if(height == null || height.length == 0) return 0;
        int l = 0;
        int r = height.length - 1;
        int lMax = height[l];
        int rMax = height[r];
        int res = 0;
        while(l < r){
            if(lMax < rMax){
                res += lMax - height[l];
                l++;
                lMax = Math.max(lMax,height[l]);
            }
            else{
                res += rMax - height[r];
                r--;
                rMax = Math.max(rMax,height[r]);
            }
        }
        return res;
    }
}
        
```

