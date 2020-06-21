# 1329. Sort the Matrix Diagonally

2020/06/21 ZLY

### Problem Description

Given a `m * n` matrix `mat` of integers, sort it diagonally in ascending order from the top-left to the bottom-right then return the sorted array.


### Algorithm

We use `x-y` to get the numbers in the same diagonal. And we use this `x-y` as a key to store the numbers in a dictionary. Then we sort the numbers according to the key. Finally, we just put the numbers back diagonal by diagonal.



### Code

```python
def diagonalSort(self, mat: List[List[int]]) -> List[List[int]]:
    row = len(mat)
    col = len(mat[0])
    data = collections.defaultdict(list)
    for i in range(row):
        for j in range(col):
            data[i-j].append(mat[i][j])
    for i in data:
        data[i].sort()
    for i in range(row):
        for j in range(col):
            mat[i][j] = data[i-j].pop(0)
    return mat
```