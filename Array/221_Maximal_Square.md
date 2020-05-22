# 221. Maximal Square

2020/05/21 ZTH

Given a 2D binary matrix filled with 0's and 1's, find the largest square containing only 1's and return its area.

**Example:**

```
Input: 

1 0 1 0 0
1 0 1 1 1
1 1 1 1 1
1 0 0 1 0

Output: 4
```



### Algorithm

* Way1 Dynamic Programming ==> O(mn) time, O(mn) space

  * allocate a dp variable with size m*n, each element store the length of the largest square up to this position (right-bottom corner)

  * detailed way:

    * 1st row

      ```
      dp[i][0] = 0 if matrix[i][0] == 0 else 1
      ```

    * 1st column

      ```
      dp[0][i] = 0 if matrix[0][i] == 0 else 1
      ```

    * other elements

      ```
      dp[i][j] = min(dp[i-1][j], dp[i][j-1], dp[i-1][j-1]) + matrix[i][j]
      
      we need to take min(dp[i-1][j], dp[i][j-1], dp[i-1][j-1]) because we need square 1s, whenever the top / left / top-left is not 1, the sqaure condition is not satisfied, we need to consider the smallest situation from the three (column, row, diagonal)
      ```

      

* Way2 Dynamic Programming ==> O(mn) time, O(n) space

  * allocate a dp vairable with size n, each element store the length of the largest square up  to this position (right-bottom corner), but we handle it row-by-row, thus require less storage space.

  * for each row

    * 1st element

      ```
      dp[0] = 0 if matrix[i][0] == 0 else 1
      ```

    * other elements

      ```
      dp[i] = min(dp[i-1], last time dp[i], last time dp[i-1]) + matrix[i][j]
      
      for last time dp[i-1], we need a separate variable to store it as we will modify dp[i-1] in the last step.
      ```

      

### Code

```python
class Solution:
    def maximalSquare(self, matrix: List[List[str]]) -> int:
        if not matrix: return 0
        # way 1: dynamic programming ==> O(mn) time, O(mn) space
        ans, dp = 0, [[0 for i in range(len(matrix[0]))] for j in range(len(matrix))]
        for i in range(len(matrix)):
            if matrix[i][0] == '1': 
                dp[i][0] = 1
                if ans < dp[i][0]: ans = dp[i][0]
        for i in range(len(matrix[0])):
            if matrix[0][i] == '1': 
                dp[0][i] = 1
                if ans < dp[0][i]: ans = dp[0][i]
        for i in range(1,len(matrix)):
            for j in range(1,len(matrix[0])):
                if matrix[i][j] == '1': 
                    dp[i][j] = min(dp[i-1][j],dp[i][j-1],dp[i-1][j-1]) + 1
                    if ans < dp[i][j]: ans = dp[i][j]
        return ans**2
                    
        
                    
```

```python
class Solution:
    def maximalSquare(self, matrix: List[List[str]]) -> int:
        if not matrix: return 0
        # way 2: dynamic programming ==> O(mn) time, O(n) space
        ans, dp = 0, [0 for i in range(len(matrix[0]))]
        for i in range(len(matrix[0])):
            if matrix[0][i] == '1':
                dp[i] = 1
                if ans < dp[i]: ans = dp[i]
        for i in range(1, len(matrix)):
            previous = dp[0]
            for j in range(len(matrix[0])):
                tmp = dp[j]
                if j == 0:
                    if matrix[i][j] == '1':
                        dp[j] = 1
                        if ans < dp[j]: ans = dp[j]
                    else: dp[j] = 0
                else:
                    if matrix[i][j] == '1':
                        dp[j] = min(dp[j-1],dp[j],previous) + 1
                        if ans < dp[j]: ans = dp[j]
                    else: dp[j] = 0
                previous = tmp
        return ans ** 2
```

