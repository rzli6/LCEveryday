# 56. Merge Intervals

2020/06/24 ZTH

### Problem Description

Given a collection of intervals, merge all overlapping intervals.

**Example 1:**

```
Input: [[1,3],[2,6],[8,10],[15,18]]
Output: [[1,6],[8,10],[15,18]]
Explanation: Since intervals [1,3] and [2,6] overlaps, merge them into [1,6].
```

**Example 2:**

```
Input: [[1,4],[4,5]]
Output: [[1,5]]
Explanation: Intervals [1,4] and [4,5] are considered overlapping.
```

**NOTE:** input types have been changed on April 15, 2019. Please reset to default code definition to get new method signature.



### Algorithm

* Sort the given input in ascending order, if there is a tie in the 1st element, then sort the 2nd.

* Once we get the sorted list, we keep two pointers left, right to record the left and right boundary of current interval.

  ```
  Initially: left = intervals[0][0]; right = intervals[0][1]
  
  For all other elements e in intervals, we iterate one by one:
  	if e[0] > right ==> no overlap, put [left, right] to results
  	if e[0] <= right ==> update right by max(r, e[1]) for the merged new intervals
  	
  ```

  Note that as the list is sorted, we do not need to compare e[0] with left as e[0] >= left

* Complexity Analysis

  * Time: O(nlogn) for sort
  * Space: O(n)



### Code

```python
class Solution:
    def merge(self, intervals: List[List[int]]) -> List[List[int]]:
        if not intervals: return intervals
        intervals.sort()
        ans, l, r = [], intervals[0][0], intervals[0][1]
        for i in range(1, len(intervals)):
            if intervals[i][0] <= r: r = max(r, intervals[i][1])
            else:
                ans.append([l,r])
                l, r = intervals[i][0], intervals[i][1]
        ans.append([l,r])
        return ans
```

