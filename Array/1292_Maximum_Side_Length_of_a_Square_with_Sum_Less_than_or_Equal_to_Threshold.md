# 1292. Maximum Side Length of a Square with Sum Less than or Equal to Threshold

2020/06/17 ZLY

### Problem Description

Given a `m x n` matrix `mat` and an integer `threshold`. Return the maximum side-length of a square with a sum less than or equal to `threshold` or return **0** if there is no such square.



### Algorithm

Two key ideas: 1) Prefix Sum; 2) Binary Search.

We can just use a new matrix to store the prefix sum of the original matrix.

And to find the max length, we use binary search. Each time we calculate the square sum, we use the prefix sum to help the calculation (in the newly-defined function `getMaxPoolVal`).



### Code

```python
def maxSideLength(self, mat: List[List[int]], threshold: int) -> int:
    def getMaxPoolVal(matrix,length,r,c,thres):
        for i in range(r-length+1):
            for j in range(c-length+1):
                square = matrix[i+length][j+length]-matrix[i][j+length]-matrix[i+length][j] + matrix[i][j]
                if square <= threshold:
                    return True
        return False
    row = len(mat)
    if row == 0:
        return 0
    col = len(mat[0])
    preSum = [[0 for _ in range(col+1)] for _ in range(row+1)]
    for i in range(1,row+1):
        sums = 0
        for j in range(1,col+1):
            sums += mat[i-1][j-1]
            preSum[i][j] = preSum[i-1][j] + sums
    result = min(row,col)
    low = 0
    high = result
    while low <= high:
        mid = (low+high)//2
        if getMaxPoolVal(preSum,mid,row,col,threshold):
            low = mid+1
        else:
            high = mid-1
    return high
```