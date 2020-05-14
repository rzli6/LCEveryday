# 80. Remove Duplicates from Sorted Array II

2020/05/13 ZTH

### Problem Description

Given a sorted array *nums*, remove the duplicates [**in-place**](https://en.wikipedia.org/wiki/In-place_algorithm) such that duplicates appeared at most *twice* and return the new length.

Do not allocate extra space for another array, you must do this by **modifying the input array [in-place](https://en.wikipedia.org/wiki/In-place_algorithm)** with O(1) extra memory.

### Algorithm

* Way 1. **One Pointer**. Scan the list once and check whether exists 3 consecutive same elements. if yes, remove the third element of the three. 
  * Time complexity O(N)
  * Space complexity O(1)

* Way 2.  **Two Pointers.** Scan the list once. one pointer <u>valid</u> keeps the position, from start to where the list satisfies the requirement. Another pointer <u>replace</u> keeps moving forward. Each time compare <u>replace</u> with <u>valid - 2</u> 

  * if not the same, replace <u>valid</u> with <u>replace</u> and both pointers increment one.
  * otherwise, <u>valid</u> not change, <u>replace</u> move one step
  * Time complexity O(N)
  * Space complexity O(1)

  > https://leetcode.com/problems/remove-duplicates-from-sorted-array-ii/discuss/386782/Three-Solutions-in-Python-3-(beats-~99)



### Code

```python
# way 1
class Solution:
    def removeDuplicates(self, nums: List[int]) -> int:
        if len(nums) < 3: return len(nums)
        valid = 2
        
        while valid < len(nums):
            if nums[valid] != nums[valid-2] or nums[valid] != nums[valid-1]:
                valid += 1
            else:
                nums.pop(valid)
        return valid                 

# way 2
class Solution:
    def removeDuplicates(self, nums: List[int]) -> int:
        if len(nums) < 3: return len(nums)
        valid = 2
        for replace in range(2, len(nums)):
            if nums[replace] > nums[valid - 2]:
                nums[valid] = nums[replace]
                valid += 1
        return valid
```