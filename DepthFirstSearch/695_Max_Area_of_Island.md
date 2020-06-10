### [695. Max Area of Island](https://leetcode.com/problems/max-area-of-island/)
Author: Ruizhe Li  
Date: 06/10/2020

#### Solution:
DFS for each cell where there is a "1" to calculate the area for each island. And find the max area among them.

#### Code:
```python
class Solution:
    def maxAreaOfIsland(self, grid: List[List[int]]) -> int:
        if not grid:
            return 0
        self.grid = grid
        self.m, self.n = len(grid), len(grid[0])
        
        def area(i, j):
            if i < 0 or i >= self.m \
                or j < 0 or j >= self.n \
                or grid[i][j] == 0:
                    return 0
                
            grid[i][j] = 0
            
            return area(i-1, j) + area(i+1, j) + area(i, j-1) + area(i, j+1) + 1
        
        area = [area(i, j) for i in range(self.m) for j in range(self.n) if grid[i][j]]
        
        return max(area) if area else 0
                
```