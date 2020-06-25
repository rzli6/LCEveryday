# 1343. Number of Sub-arrays of Size K and Average Greater than or Equal to Threshold

2020/06/24 ZLY

### Problem Description

Given an array of integers `arr` and two integers `k` and `threshold`.

Return *the number of sub-arrays* of size `k` and average greater than or equal to `threshold`.




### Algorithm

First, we calculate the sum of the first subarray. Then everytime we just subtract the head from the sum and also add the tail to get the new sum. If the sum is >= k*threshold, then we add 1 to the result.



### Code

```python
def numOfSubarrays(self, arr: List[int], k: int, threshold: int) -> int:
    sum_threshold = threshold*k
    current_sum = 0
    result = 0
    for i in range(k):
        current_sum += arr[i]
    if current_sum >= sum_threshold:
        result += 1
    for i in range(len(arr)-k):
        current_sum = current_sum - arr[i] + arr[i+k]
        if current_sum >= sum_threshold:
            result += 1
  return result
```