# 64. Minimum Path Sum

2020/05/19 ZTH

### Problem Description

Given a *m* x *n* grid filled with non-negative numbers, find a path from top left to bottom right which *minimizes* the sum of all numbers along its path.

**Note:** You can only move either down or right at any point in time.

e.g.

```
Input:
[
  [1,3,1],
  [1,5,1],
  [4,2,1]
]
Output: 7
Explanation: Because the path 1→3→1→1→1 minimizes the sum.
```



### Algorithm

Dynamic Programming ==> bottom up ==> O(*mn*) time, O(1) space (# no extra space).

* for the first row & first column

  * Current minimum path sum is current position value + previous value

    ```
    grid[i][0] += grid[i-1][0] # for 1st column
    grid[0][i] += grid[0][i-1] # for 1st row
    ```

* for other elements

  * Current minimum path sum is the minimum one of its top or left element + its current value

    ```
    grid[i][j] += min(grid[i-1][j],grid[i][j-1])
    ```

    

### Code

```python
class Solution:
    def minPathSum(self, grid: List[List[int]]) -> int:
        # special case for emptu grid
        if not grid: return 0
        for i in range(1,len(grid[0])):
            grid[0][i] += grid[0][i-1]
        for i in range(1,len(grid)):
            grid[i][0] += grid[i-1][0]
        
        for i in range(1,len(grid)):
            for j in range(1,len(grid[0])):
                grid[i][j] += min(grid[i-1][j],grid[i][j-1])
        return grid[-1][-1]
```

