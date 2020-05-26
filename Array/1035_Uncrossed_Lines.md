### 1035. Uncrossed Lines
Link: https://leetcode.com/problems/uncrossed-lines/   
Code: https://colab.research.google.com/drive/1zwh7pppur0pIoEgi3mNOI3cRV9GBBZ0E?usp=sharing  
Author: Ruizhe Li  
Date: 05/26/2020  

#### Solution:
**Dynamic Programming**  
The result of A[1:i] and B[1:j] can be divided into subproblems:
* result of A[1:i-1] and B[1:j-1] + 1, if A[i] == B[j]
* max of result of A[1:i-1] and B[1:j] and result of A[1:i] and B[1:j-1]

#### Code:
```python
class Solution:
  def maxUncrossedLines(self, A: List[int], B: List[int]) -> int:
    m, n = len(A), len(B)

    # initialize a dp array
    # 1-d array is enough as the result of current row only depends
    # on the row one level up
    dp = [0]*(n+1)

    for i in range(m):
      for j in range(n)[::-1]: # from back to front
        if A[i] == B[j]:
          dp[j+1] = dp[j] + 1
      for j in range(n): 
        dp[j+1] = max(dp[j+1], dp[j])
    return dp[n]
```