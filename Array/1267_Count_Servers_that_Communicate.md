# 1267. Count Servers that Communicate

2020/06/16 ZLY

### Problem Description

You are given a map of a server center, represented as a `m * n` integer matrix `grid`, where 1 means that on that cell there is a server and 0 means that it is no server. Two servers are said to communicate if they are on the same row or on the same column.

Return the number of servers that communicate with any other server.



### Algorithm

We count the number of servers each row and column. And iterate through the grid, if (there is a server) and (the number of servers on its row or column > 1), then we add 1 to the result.



### Code

```python
def countServers(self, grid: List[List[int]]) -> int:
    row = len(grid)
    col = len(grid[0])
    result = 0
    count_row = [0]*row
    count_col = [0]*col
    for i in range(row):
        for j in range(col):
            if grid[i][j]:
                count_row[i]+=1
                count_col[j]+=1
    for i in range(row):
        for j in range(col):
            if grid[i][j] and (count_row[i]>1 or count_col[j]>1):
                result += 1
    return result
```