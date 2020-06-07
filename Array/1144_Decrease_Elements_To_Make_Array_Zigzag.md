# 1144. Decrease Elements To Make Array Zigzag

2020/06/07 ZLY

### Problem Description

Given an array `nums` of integers, a *move* consists of choosing any element and **decreasing it by 1**.

An array `A` is a *zigzag array* if either:

- Every even-indexed element is greater than adjacent elements, ie. `A[0] > A[1] < A[2] > A[3] < A[4] > ...`
- OR, every odd-indexed element is greater than adjacent elements, ie. `A[0] < A[1] > A[2] < A[3] > A[4] < ...`

Return the minimum number of moves to transform the given array `nums` into a zigzag array.



### Algorithm

We consider two cases: 1) odd indexes smaller, even indexes larger; 2) odd indexes larger, even indexes smaller.

If a number needs to be smaller, we just change it to `the smaller value of its neighbors - 1`.

In the end, we can just calculate the difference between the new list and the original list, which is exactly the number of moves.



### Code

```python
def movesToMakeZigzag(self, nums: List[int]) -> int:
    tmp = nums[:]
    count = 0
    for i in range(1,len(nums),2):
        if i != len(nums)-1:
            if nums[i] >= nums[i-1] or nums[i] >= nums[i+1]:
                nums[i] = min(nums[i-1],nums[i+1]) - 1
        else:
            if nums[i] >= nums[i-1]:
                nums[i] = nums[i-1]-1
    count = sum(tmp) - sum(nums)
    nums = tmp[:]
    for i in range(0,len(nums),2):
        if i != 0 and i != len(nums)-1:
            if nums[i] >= nums[i-1] or nums[i] >= nums[i+1]:
                nums[i] = min(nums[i-1],nums[i+1]) - 1
        elif i == 0:
            if nums[i] >= nums[i+1]:
                nums[i] = nums[i+1] - 1
        else:
            if nums[i] >= nums[i-1]:
                nums[i] = nums[i-1] - 1
    count = min(count,sum(tmp)-sum(nums))
    return count
```