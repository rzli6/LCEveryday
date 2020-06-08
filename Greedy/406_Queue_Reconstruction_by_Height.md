### [406. Queue Reconstruction by Height](https://leetcode.com/problems/queue-reconstruction-by-height/)
Author: Ruizhe Li  
Date: 06/07/2020


#### Solution:
1. Sort people according to their h and (reverse) k.
1. Insert each person to its correct position from backward.

#### Code:
```python
class Solution:
  def reconstructQueue(self, people: List[List[int]]) -> List[List[int]]:
    # sort people respect to h and -k
    people.sort(key=lambda p: (p[0],-p[1]))
    
    res = []
    # from backward, insert people to its right position
    for p in people[::-1]:
      res.insert(p[1], p)
    return res
```