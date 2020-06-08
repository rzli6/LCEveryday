### 695. Max Area of Island
LC link: https://leetcode.com/problems/max-area-of-island/
Author: XDDDD
Date: 06/07/2020

#### Solution:
DFS: Generate a boolean array to record whether a land is visited or not. When doing dfs, sum up all the visited array. Inspect the max value for each found island.

#### Code:
```Java
class Solution {
    int[][] directions = {{1,0},{-1,0},{0,1},{0,-1}};
    public int maxAreaOfIsland(int[][] grid) {
        int n = grid.length;
        if(n == 0) return 0;
        int m = grid[0].length;
        if(m == 0) return 0;
        boolean[][] visited = new boolean[n][m];
        int max = 0;
        for(int i = 0;i<n;i++){
            for(int j = 0;j<m;j++){
                if(grid[i][j] == 0 || visited[i][j]) continue;
                max = Math.max(max,dfs(grid,visited,i,j));
            }
        }
        return max;
    }
    
    public int dfs(int[][] grid, boolean[][] visited, int x, int y){
        if(grid[x][y] == 0 || visited[x][y]) return 0;
        visited[x][y] = true;
        int sum = 1;
        for(int[] dir : directions){
            int x1 = x + dir[0];
            int y1 = y + dir[1];
            if(x1 < 0 || y1 < 0 || x1 >= grid.length || y1 >= grid[0].length) continue;
            sum += dfs(grid,visited,x1,y1);
        }
        return sum;
    }
}
```

