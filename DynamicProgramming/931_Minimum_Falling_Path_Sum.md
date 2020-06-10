# 931. Minimum Falling Path Sum

2020/06/09 ZTH

### Problem Description

Given a **square** array of integers `A`, we want the **minimum** sum of a *falling path* through `A`.

A falling path starts at any element in the first row, and chooses one element from each row. The next row's choice must be in a column that is different from the previous row's column by at most one.

**Example 1:**

```
Input: [[1,2,3],[4,5,6],[7,8,9]]
Output: 12
Explanation: 
The possible falling paths are:
```

- `[1,4,7], [1,4,8], [1,5,7], [1,5,8], [1,5,9]`
- `[2,4,7], [2,4,8], [2,5,7], [2,5,8], [2,5,9], [2,6,8], [2,6,9]`
- `[3,5,7], [3,5,8], [3,5,9], [3,6,8], [3,6,9]`

The falling path with the smallest sum is `[1,4,7]`, so the answer is `12`.

**Note:**

1. `1 <= A.length == A[0].length <= 100`
2. `-100 <= A[i][j] <= 100`



### Algorithm

* Algorithm1: dynamic programming O(n^2) time, O(n^2) space

  * use an additional variable ans to store the minimum sum of falling path up to this position

  * use previous row result to update this row

    ```
    Three situations
    1) 1st element in each row i: 
    			curr[0] = min(ans[i-1][0], ans[i-1][1]) + A[i][0]
    2) last element in each row i:
    			curr[n] = min(ans[i-1][n-1], ans[i-1][n]) + A[i][n]
    3) other elements in each row i:
    			curr[] = min(ans[i-1][col], ans[i-1][col-1], ans[i-1][col+1]) + A[i][col]
    ```

  * return the smallest number in the last row of ans

* Algorithm2: dynamic programming O(n^2) time, O(n) space, based on algorithm1

  * use two separate 1d array to store current and previous results for modification



### Code

```python
class Solution:
    def minFallingPathSum(self, A: List[List[int]]) -> int:
        # dynamic programming O(n^2) time, O(n^2) space
        ans = []
        for row in range(len(A)):
            if row == 0: ans.append(A[0])
            else:
                current = []
                for col in range(len(A[0])):
                    if col == 0: current.append(min(ans[row-1][col], ans[row-1][col+1]) + A[row][col])
                    elif col == len(A[0]) - 1: current.append(min(ans[row-1][col-1], ans[row-1][col]) + A[row][col])
                    else: current.append(min(ans[row-1][col], ans[row-1][col-1], ans[row-1][col+1]) + A[row][col])
                ans.append(current)
        return min(ans[-1])
```



```python
class Solution:
    def minFallingPathSum(self, A: List[List[int]]) -> int:
        # dynamic programming O(n^2) time, O(n) space
        pre, curr = [], []
        for row in range(len(A)):
            if row == 0: curr = A[0]
            else:
                curr = []
                for col in range(len(A[0])):
                    if col == 0: curr.append(min(pre[col], pre[col+1]) + A[row][col])
                    elif col == len(A[0]) - 1: curr.append(min(pre[col-1], pre[col]) + A[row][col])
                    else: curr.append(min(pre[col-1], pre[col], pre[col+1]) + A[row][col])
            pre = curr
        return min(curr)
                                                                                        
                
```

