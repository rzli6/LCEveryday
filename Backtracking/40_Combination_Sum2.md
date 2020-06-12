# 40. Combination Sum II

Author: zhuofei  
date: 6.12  
rating: 3.0/5.0  

## Problem
Given a collection of candidate numbers (candidates) and a target number (target), find all unique combinations in candidates where the candidate numbers sums to target.

Each number in candidates may only be used once in the combination.

Note:

All numbers (including target) will be positive integers.
The solution set must not contain duplicate combinations.
Example 1:
```
Input: candidates = [10,1,2,7,6,1,5], target = 8,
A solution set is:
[
  [1, 7],
  [1, 2, 5],
  [2, 6],
  [1, 1, 6]
]
```

## Difficulty

1. Consider 3 or more duplicate candidates (should think before start)

2. "Each number in candidates may only be used **once** in the combination."

    - How to do? when selecting number, make sure we only select unique number once to add in the list  
    - Honestly, it means we do not add same number in the same helper function  
    - The first duplicate number can call helper function to add same number, if there are three 1, the first 1 can add the second and third, the second can only add third, and the third can only add itself.  
    - It's important to study the core idea of it. Now I cannot summerize and make clear. 

## Backtracking
It's better to compare the code between 39 and 40.
```python
class Solution:
    def helper(self, candidates: List[int], target: int, cur_set: List[int], index: int, res: List[List[int]]):
        if target == 0:
            res.append(cur_set)
        if target < 0:
            return
        for i in range(index, len(candidates)):
            if i > index and candidates[i] == candidates[i-1]:
                continue
            self.helper(candidates, target-candidates[i], cur_set+[candidates[i]], i+1, res)
    
    def combinationSum2(self, candidates: List[int], target: int) -> List[List[int]]:
        candidates.sort()
        res = []
        # recursive
        self.helper(candidates, target, [], 0, res)      
        return res  
```

## Dynamic Programming [TODO]