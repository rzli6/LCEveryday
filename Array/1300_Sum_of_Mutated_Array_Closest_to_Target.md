# 1300. Sum of Mutated Array Closest to Target

2020/06/20 ZLY

### Problem Description

Given an integer array `arr` and a target value `target`, return the integer `value` such that when we change all the integers larger than `value` in the given array to be equal to `value`, the sum of the array gets as close as possible (in absolute difference) to `target`.

In case of a tie, return the minimum such integer.

Notice that the answer is not neccesarilly a number from `arr`.




### Algorithm

We can find out that the final result is in the range between 0 and `max(arr)`. Therefore, we can just use binary search to get the value.



### Code

```python
def findBestValue(self, arr: List[int], target: int) -> int:
    low = 0
    high = max(arr)
    min_difference = float('inf')
    result = float('inf')
    while low <= high:
        mid = (low + high) // 2
        new_sum = 0
        for num in arr:
            if num > mid:
                new_sum += mid
            else:
                new_sum += num
        difference = abs(new_sum-target)
        if difference < min_difference:
            min_difference = difference
            result = mid
        elif difference == min_difference:
            result = min(result, mid) # in case of a tie
        if new_sum > target:
            high = mid - 1
        elif new_sum < target:
            low = mid + 1
        else:
            return mid
    return result
```