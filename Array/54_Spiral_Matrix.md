# 54. Spiral Matrix

2020/06/29 ZTH

### Problem Description

Given a matrix of *m* x *n* elements (*m* rows, *n* columns), return all elements of the matrix in spiral order.

**Example 1:**

```
Input:
[
 [ 1, 2, 3 ],
 [ 4, 5, 6 ],
 [ 7, 8, 9 ]
]
Output: [1,2,3,6,9,8,7,4,5]
```



### Algorithm

* Truncate the spiral order matrix into iteration access, where each iteration 1) first goes from left -> right; 2) goes from up -> down; 3) goes from right -> left; 4) goes from down -> up if necessary.

  ```
  [
   [ 1, 2, 3 ],
   [ 4, 5, 6 ],
   [ 7, 8, 9 ]
  ]
  
  1st: 1,2,3 -> 6,9 -> 8,7 -> 4
  2nd: 5 (no element left)
  ```

* The normal iteration i has the following index procedure:

  ```
  assume m rows and n columns
  for one iteration
  1) left -> right: [i, i], [i, i+1], ..., [i, n-i-1]
  2) up -> down:		[i+1, n-i-1], [i+2, n-i-1], ..., [m-i-1, n-i-1] 
  									column is fixed, = 1)'s last column index
  									row starts with 1)'s column + 1
  3) right -> left: [m-i-1, n-i-1-1], ... ,[m-i-1, i]
  									row is fiexd, = 2)'s last column index
  									column starts with 2)'s column - 1
  4) down -> up:    [m-i-1-1, i], ..., [i+1, i]
  									column is fixed, = 3)'s last column index
  									row starts with 3)'s row - 1
  ```

* The above method works well when m == n, but involves repeate access when m != n. To deal with the problem, use another variable seen with size m x n to record the status whether we access each element before. We only put unseen element to final answer.

* Complexity Analysis

  * Time: O(mxn)
  * Space: O(mxn)



### Code

```python
class Solution:
    def spiralOrder(self, matrix: List[List[int]]) -> List[int]:
        if not matrix: return []
        m, n, ans = len(matrix), len(matrix[0]), []
        seen = [[False for i in range(n)] for j in range(m)]
        for i in range(min(m,n)):
            for c in range(i, n-i): 
                if not seen[i][c]:
                    ans.append(matrix[i][c])
                    seen[i][c] = True
            for r in range(i+1, m-i): 
                if not seen[r][n-i-1]:
                    ans.append(matrix[r][n-i-1])
                    seen[r][n-i-1] = True
            for c in range(n-i-1-1, i-1, -1): 
                if not seen[m-i-1][c]:
                    ans.append(matrix[m-i-1][c])
                    seen[m-i-1][c] = True
            for r in range(m-i-1-1, i, -1): 
                if not seen[r][i]:
                    ans.append(matrix[r][i])
                    seen[r][i] = True
        return ans
        
```

