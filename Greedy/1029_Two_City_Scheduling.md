### [1029. Two City Scheduling](https://leetcode.com/problems/two-city-scheduling/)
Author: Ruizhe Li  
Date: 06/04/2020

#### Solution:
Greedy Algorithm: 
* Sort the list in terms of the cost increment if we put a person in A rather than B. 
* Put the first half of the sorted list in A and second half in B.

#### Code:
```python
class Solution:
  def twoCitySchedCost(self, costs: List[List[int]]) -> int:
    diff = [a-b for a, b in costs]
    dc = sorted(zip(diff, costs), key = lambda x: x[0])
    mid = len(dc) // 2
    return sum(c[0] for d, c in dc[:mid]) + sum(c[1] for d, c in dc[mid:])
```