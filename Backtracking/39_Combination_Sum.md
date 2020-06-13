# 39. Combination Sum [Unfinished]

Author: zhuofei  
date: 6.11  
rating: 3.0/5.0  

## Problem
Given a set of candidate numbers (candidates) (without duplicates) and a target number (target), find all unique combinations in candidates where the candidate numbers sums to target.

The same repeated number may be chosen from candidates unlimited number of times.

Note:

All numbers (including target) will be positive integers.
The solution set must not contain duplicate combinations.
Example 1:
```
Input: candidates = [2,3,6,7], target = 7,
A solution set is:
[
  [7],
  [2,2,3]
]
```

## Backtracking

```python
class Solution:    
    def helper(self, candidates: List[int], target: int, cur_set: List[int], index: int, res: List[List[int]]):
        for i in range(index, len(candidates)):
            if target - candidates[i] > 0:
                self.helper(candidates, target-candidates[i], cur_set+[candidates[i]], i, res)
            elif target == candidates[i]:
                res.append(cur_set+[candidates[i]])
            else:
                break
    
    def combinationSum(self, candidates: List[int], target: int) -> List[List[int]]:
        candidates.sort()
        res = []
        # recursive
        self.helper(candidates, target, [], 0, res)      
        return res 
```