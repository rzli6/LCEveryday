# 34. Find First and Last Position of Element in Sorted Array

2020/05/11 ZTH

### Problem Description

Given an array of integers `nums` sorted in ascending order, find the starting and ending position of a given `target` value.

Your algorithm's runtime complexity must be in the order of *O*(log *n*).

If the target is not found in the array, return `[-1, -1]`.

### Algorithm

1. Use binary search to find a position of target

2. Based on the position found in last step

   - Binary search of the left part of the position to find the start point

     - Three cases when binary search left part:

       ```python
       (1) continue updating left indicator until nums[mid] == target
       (2) if nums[mid] == target and nums[mid-1] < target: return mid
       (3) if nums[mid] == target and nums[mid-1] == target: update right indicator
       ```

   - Binary search of the right part of the position to find the end point (same as left part)

3. Return [start, end]

*Pay attention to special cases: empty list etc.*

