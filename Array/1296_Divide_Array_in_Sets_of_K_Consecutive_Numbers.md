# 1296. Divide Array in Sets of K Consecutive Numbers

2020/06/18 ZLY

### Problem Description

Given an array of integers `nums` and a positive integer `k`, find whether it's possible to divide this array into sets of `k` consecutive numbers
Return `True` if its possible otherwise return `False`.



### Algorithm

We first sort the nums, and every time we consider nums[0] as the first number and search altogether k numbers.

We check whether all numbers in this k-numbers group exist. If not, just directly return False.

Until all the numbers in nums is checked, we can return True.



### Code

```python
def isPossibleDivide(self, nums: List[int], k: int) -> bool:
    from collections import Counter, deque
    dic = Counter(nums)
    nums = deque(sorted(list(set(nums))))
    result = []
    while nums:
        num = nums[0]
        for i in range(k):
            target = num + i
            if target not in dic:
                return False
            dic[target] -= 1
            if dic[target] == 0:
                nums.popleft()
    return True
```