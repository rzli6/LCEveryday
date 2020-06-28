# 334. Increasing Triplet Subsequence

2020/06/28 ZTH

### Problem Description

Given an unsorted array return whether an increasing subsequence of length 3 exists or not in the array.

Formally the function should:

> Return true if there exists *i, j, k*
> such that *arr[i]* < *arr[j]* < *arr[k]* given 0 ≤ *i* < *j* < *k* ≤ *n*-1 else return false.

**Note:** Your algorithm should run in O(*n*) time complexity and O(*1*) space complexity.

**Example 1:**

```
Input: [1,2,3,4,5]
Output: true
```

**Example 2:**

```
Input: [5,4,3,2,1]
Output: false
```



### Algorithm

* Note that any subsequence ==> no need to be continuous subarray
* Use two variables first, second to store the smallest and middle element of the triplet, initialized as infinite at the beginning.
* Iterate the given list
  *  first check whether element <= first, if yes ==> update first
  * check whether element > first and element <= second, if yes ==> update second
  * otherwise, we found the third element / largest element of the triplet, return True directly.
* Complexity Analysis
  * Time: O(n), iterate list once
  * Space: O(1)



### Code

```python
class Solution:
    def increasingTriplet(self, nums: List[int]) -> bool:
        if len(nums) < 3: return False
        first = second = float('inf')
        for e in nums:
            # smallest number in the triplet
            if e <= first: first = e
            # middle number in the triplet
            elif e <= second: second = e
            # find the triplet
            else: return True
        return False
        
```

