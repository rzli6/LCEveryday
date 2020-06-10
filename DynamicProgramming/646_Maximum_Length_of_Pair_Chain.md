# 646. Maximum Length of Pair Chain

2020/06/10 ZTH

### Problem Description

You are given `n` pairs of numbers. In every pair, the first number is always smaller than the second number.

Now, we define a pair `(c, d)` can follow another pair `(a, b)` if and only if `b < c`. Chain of pairs can be formed in this fashion.

Given a set of pairs, find the length longest chain which can be formed. You needn't use up all the given pairs. You can select pairs in any order.

**Example 1:**

```
Input: [[1,2], [2,3], [3,4]]
Output: 2
Explanation: The longest chain is [1,2] -> [3,4]
```



**Note:**

1. The number of given pairs will be in the range [1, 1000].



### Code

```python
class Solution:
    def findLongestChain(self, pairs: List[List[int]]) -> int:
        dp = [1] * len(pairs)
        pairs.sort()
        
        for end in range(len(pairs)):
            for index in range(end):
                if pairs[index][1] < pairs[end][0]: dp[end] = max(dp[index]+1, dp[end]) 
        return max(dp)
        
```

