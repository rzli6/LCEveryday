# 238. Product of Array Except Self

2020/05/14 ZTH

### Problem Description

Given an array `nums` of *n* integers where *n* > 1,  return an array `output` such that `output[i]` is equal to the product of all the elements of `nums` except `nums[i]`.

e.g.

```
Input:  [1,2,3,4]
Output: [24,12,8,6]
```

### Algorithms

* Way 1: 2 Lists Approach. 

  O(n) time, O(n) space (2 scans, 2 lists)

  For each position i, we use two lists, one store the product from position 0 to position (i-1); the other store the product from position (i+1) to position (len(nums)-1). The final result is element-wise production of the two lists.

  * Left List: left[0] = 1, no element on the left; left[1] = left[0] * nums[0], ... left[i] = left[i-1] * nums[i-1]
  * Right List: right[len(nums)-1] = 1, no element on the right; right[len(nums)-2] = right[len(nums)-1] * nums[len(nums)-2]
  * Result: result[i] = left[i] * right[i]

* Way 2: 1 list Approach

  O(n) time, O(1) space (except the ans list)

  Based on approach 1, one list is used, first store the product from position 0 to position (i-1) (similar like left in previous), and use one variable for store each value of the right.

  * ans List: ans[0] = 1, no element on the left; ans[1] = ans[0] * nums[0], ... ans[i] = ans[i-1] * nums[i-1]
  * For the right: set previous = 1, for i start from len(nums)-1, ans[i] *= previous, set previous = previous * nums[i]



### Codes

```python
# way 1 2 Lists Approach
class Solution:
    def productExceptSelf(self, nums: List[int]) -> List[int]:
        left, right = [1], [1]
        for i in range(len(nums)-1):
            left.append(left[i] * nums[i])
        for i in range(len(nums)-1, 0, -1):
            right.insert(0,nums[i]*right[0])
        for i in range(len(left)):
            left[i] = left[i] * right[i]
        return left
```

```python
class Solution:
    def productExceptSelf(self, nums: List[int]) -> List[int]:
        ans, previous = [1], 1
        for i in range(len(nums)-1):
            ans.append(ans[i]*nums[i])
        for i in range(len(nums)-1, 0, -1):
            ans[i] *= previous
            previous *= nums[i]
        ans[0] *= previous
        return ans
```

