### [1229. Meeting Scheduler](https://leetcode.com/problems/meeting-scheduler/)
Author: Ruizhe Li  
Date: 06/05/2020  

#### Solution:
Standard **line sweep** algorithm.
1. Sort the two lists respects to their ending time.
1. Start from beginning of two lists:
  * If the intercept of the two slots are bigger or equal to the duration, return start time and start time + duration.
  * Otherwise, find the one with smaller end time and move the pointer one step forward.  

#### Code:
```python
class Solution:
  def minAvailableDuration(self, slots1: List[List[int]], slots2: List[List[int]], duration: int) -> List[int]:
    # sort the two lists
    slots1.sort(key=lambda x: x[0])
    slots2.sort(key=lambda x: x[1])
    
    # start from beginning
    i, j = 0, 0

    # while the pointers are still in the range
    while i < len(slots1) and j < len(slots2):
      # get intersection
      start = max(slots1[i][0], slots2[j][0])
      end = min(slots1[i][1],slots2[j][1])

      # get length of interval
      if end - start >= duration:
        return [start, start+duration]
      
      # move the pointer of the early-ending one forward
      if slots1[i][1] < slots2[j][1]:
        i += 1
      else:
        j += 1
    
    # impossible to satisfy the requirement
    return []
```