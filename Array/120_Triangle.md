# 120. Triangle

2020/05/20 ZTH

### Problem Description

Given a triangle, find the minimum path sum from top to bottom. Each step you may move to adjacent numbers on the row below.

For example, given the following triangle

e.g.

```
[
     [2],
    [3,4],
   [6,5,7],
  [4,1,8,3]
]
```

The minimum path sum from top to bottom is `11` (i.e., **2** + **3** + **5** + **1** = 11).

**Note:**

Bonus point if you are able to do this using only *O*(*n*) extra space, where *n* is the total number of rows in the triangle.



### Algorithm

* **Way1 Dynamic Programming ==> O(n^2) time, O(n^2) space**

  * allocate triangle-sized extra space to store the results

  * each element stores the minimum path sum from top to current position

    * first row: single element, simply itself
    * other rows:
      * 1st element: itself + previous row 1st element result
      * last elemnt: itself + previous row last element result
      * other elements: itself + min(previous row i-1 position result, previous row current position result)

  * return minimum result of last row

  * time & space: 1+2+3+...+n = n(n+1)/2, n = # rows

    

* **Way 2 Dynamic Programming ==> O(n^2) time, O(1) extra space**

  * similar as Way1, but use the input triangle variable to store the results by in-place modification



### Code

```python
class Solution:
    def minimumTotal(self, triangle: List[List[int]]) -> int:
        # way1: O(n^2) time, O(n^2) space
        if not triangle: return 0
        result = [[triangle[0][0]]]
        for row in range(1, len(triangle)):
            current = [result[row-1][0] + triangle[row][0]]
            for i in range(1,row):
                current.append(min(result[row-1][i-1],result[row-1][i])+triangle[row][i])
            current.append(result[row-1][-1] + triangle[row][-1])
            result.append(current)
        return min(result[-1])
```

```python
class Solution:
    def minimumTotal(self, triangle: List[List[int]]) -> int:
        if not triangle: return 0
        for row in range(1, len(triangle)):
            triangle[row][0] += triangle[row-1][0]
            for i in range(1,row):
                triangle[row][i] += min(triangle[row-1][i-1],triangle[row-1][i])
            triangle[row][-1] += triangle[row-1][-1]
        return min(triangle[-1])
```

