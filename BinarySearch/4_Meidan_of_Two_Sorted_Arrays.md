# 4. Median of Two Sorted Arrays

Author: LIU Zhuofei  
Date: 2020.5.28  
Rating: 4.0/5.0  

## Problem
There are two sorted arrays **nums1** and **nums2** of size **m** and **n** respectively.

Find the median of the two sorted arrays. The overall run time complexity should be **O(log (m+n))**.

You may assume **nums1** and **nums2** cannot be both empty.

Example 1:  
```
nums1 = [1, 2]
nums2 = [3, 4]

The median is (2 + 3)/2 = 2.5
```

## Idea

1. Solutiton is based on binary search because of time complexity  
2. Binary search on one array is **O(log (n))**  
3. If we consider two arrays, A and B, as one set, we can divide it into two sets **Left** and **Right** with same number of elements, or size(Left) = size(Right) + 1. Any elements in **Left** should smaller than or equal to any elements in **Right**.
4. We have low, mid, high variables to record indexes in array using normal binary search. In another array B, ```mid_in_B = (A.length+B.length+1)/2 - mid_in_A;```
5. That's the way we ensure point 3 successes. Since array A and B is sorted, we only need to make sure 
   ```
   A[mid_in_A-1] < B[mid_in_B]
   A[mid_in_A] > B[mid_in_B-1]
   ```
6. The following is to consider three cases to make **mid** move left or right, or one of the whole array is in the **Left** or **Right**  
7. **mid**:
   1. A[mid_in_A-1] > B[mid_in_B], mid_in_A need increase
   2. A[mid_in_A] < B[mid_in_B-1], mid_in_A need decrease
8. when we find one of the whole array is in the **Left** or **Right**, It will be much easier.