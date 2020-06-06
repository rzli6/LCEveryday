# 739. Daily Temperatures

2020/06/06 ZTH

### Problem Description

Given a list of daily temperatures `T`, return a list such that, for each day in the input, tells you how many days you would have to wait until a warmer temperature. If there is no future day for which this is possible, put `0` instead.

For example, given the list of temperatures `T = [73, 74, 75, 71, 69, 72, 76, 73]`, your output should be `[1, 1, 4, 2, 1, 1, 0, 0]`.

**Note:** The length of `temperatures` will be in the range `[1, 30000]`. Each temperature will be an integer in the range `[30, 100]`.



### Algorithm

* to get the next greater element position, we could store each elements occurrence position
* start from the last one, for each item use a variable to store its next occurrence position
  * when process each item, check next occurrence of value k (item + 1 <= k <= 100), and keep the smallest one
  * the next occurrence of the value k could only be invalid number or an index larger than current i
* Complexity Analysis
  * Time: O(N) ==> O(70N)
  * Space: O(N)



### Code

```python
class Solution:
    def dailyTemperatures(self, T: List[int]) -> List[int]:
      # pos store the next occurrence
        ans, pos = [0] * len(T), [len(T)] * 101
        for i in range(len(T)-1, -1, -1):
            nex = min(pos[k] for k in range(T[i],101)) # nex > i
            if nex < len(T): ans[i] = (nex - i)
            pos[T[i]-1] = i # update pos when process each item
        return ans
```

