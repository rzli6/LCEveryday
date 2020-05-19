# 63. Unique Paths II

2020/05/18 ZTH

### Problem Description

A robot is located at the top-left corner of a *m* x *n* grid (marked 'Start' in the diagram below).

The robot can only move either down or right at any point in time. The robot is trying to reach the bottom-right corner of the grid (marked 'Finish' in the diagram below).

Now consider if some obstacles are added to the grids. How many unique paths would there be?

An obstacle and empty space is marked as `1` and `0` respectively in the grid.

**Note:** *m* and *n* will be at most 100.

e.g.

```
Input:
[
  [0,0,0],
  [0,1,0],
  [0,0,0]
]
Output: 2
Explanation:
There is one obstacle in the middle of the 3x3 grid above.
There are two ways to reach the bottom-right corner:
1. Right -> Right -> Down -> Down
2. Down -> Down -> Right -> Right
```



### Algorithm



```
m, n = len(obstacleGrid), len(obstacleGrid[0])
```



1. **Way 1 Dynamic Programming** ==> O(*mn*) time, O(*mn*) space

* start from beginning to the end, initialize all elements of the box to 0

* allocate a *mxn* box to store # of possible unique paths of each position

  * the first row (*m=1*) & first column (*n=1*) elements are set to 1 is the position obstacleGrid[i] = 0; once the position obstacleGrid[i] = 1, stop

  * for other positions, iterate the 2d loops and fill elements one by one from the top-left to bottom-right: 

    ``` 
    if obstacleGrid[i][j] == 0: # no obstacle
    	box[i][j] = box[i-1][j] + box[i][j-1]
    ```

2. **Way 2 Dynamic Programming** ==> O(*mn*) time, O(*1*) space

* similar as way1, but we utilize the input obstacleGrid instead of allocating new matrix memory for storage

* for the first row and first column

  * we set element to 1 if the position obstacleGrid[i] = 0; else set element to 0 if the position obstacleGrid[i] = 1; once there is one 1 in the row / column, all following elements are 0

    ```
    for i in range(1,len(obstacleGrid) or len(obstacleGrid[0])):
    	if status1 and obstacleGrid[i][0] == 0: obstacleGrid[i][0] = 1
      else:
      	obstacleGrid[i][0] = 0
        status1 = 0
    ```

  * for other positions, iterate the 2d loops and fill elements one by one from top-left to bottom-right. 

    ```
    if obstacleGrid[i][j] == 0: obstacleGrid[i][j] = obstacleGrid[i-1][j] + obstacleGrid[i][j-1]
    else: obstacleGrid[i][j] = 0
    ```



### Code

```python
class Solution:
    def uniquePathsWithObstacles(self, obstacleGrid: List[List[int]]) -> int:
        if not obstacleGrid: return 0
        if obstacleGrid[0][0] == 1: return 0
        if len(obstacleGrid) == 1 and len(obstacleGrid[0]) == 1: return 1 if obstacleGrid[0][0] == 0 else 0
        # way 1: dynamic programming ==> O(mn) time, O(mn) space
        box = [[0 for i in range(len(obstacleGrid[0]))] for j in range(len(obstacleGrid))]
        for i in range(1, len(obstacleGrid)):
            if obstacleGrid[i][0] == 0: box[i][0] = 1
            else: break
        for i in range(1,len(obstacleGrid[0])):
            if obstacleGrid[0][i] == 0: box[0][i] = 1
            else: break
        for i in range(1,len(obstacleGrid)):
            for j in range(1,len(obstacleGrid[0])):
                if obstacleGrid[i][j] == 0:
                    box[i][j] = box[i-1][j] + box[i][j-1]
        return box[-1][-1]
```

```python
class Solution:
    def uniquePathsWithObstacles(self, obstacleGrid: List[List[int]]) -> int:
        if not obstacleGrid: return 0
        if obstacleGrid[0][0] == 1: return 0
        if len(obstacleGrid) == 1 and len(obstacleGrid[0]) == 1: return 1 if obstacleGrid[0][0] == 0 else 0

        status1, status2 = 1, 1
        for i in range(1,len(obstacleGrid)):
            if status1 and obstacleGrid[i][0] == 0: obstacleGrid[i][0] = 1
            else:
                obstacleGrid[i][0] = 0
                status1 = 0
        for i in range(1,len(obstacleGrid[0])):
            if status2 and obstacleGrid[0][i] == 0: obstacleGrid[0][i] = 1
            else:
                obstacleGrid[0][i] = 0
                status2 = 0
        for i in range(1, len(obstacleGrid)):
            for j in range(1, len(obstacleGrid[0])):
                if obstacleGrid[i][j] == 0: obstacleGrid[i][j] = obstacleGrid[i-1][j] + obstacleGrid[i][j-1]
                else: obstacleGrid[i][j] = 0
        return obstacleGrid[-1][-1]
                    
```



### Special Cases

```
1. Empty obstacleGrid ==> 0
2. The start position has obstacle ==> 0
3. The end position has obstacle ==> 0
```

