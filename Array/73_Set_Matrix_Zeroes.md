# 73. Set Matrix Zeroes

2020/06/27 ZTH

Given a *m* x *n* matrix, if an element is 0, set its entire row and column to 0. Do it [**in-place**](https://en.wikipedia.org/wiki/In-place_algorithm).

**Example 1:**

```
Input: 
[
  [1,1,1],
  [1,0,1],
  [1,1,1]
]
Output: 
[
  [1,0,1],
  [0,0,0],
  [1,0,1]
]
```

**Follow up:**

- A straight forward solution using O(*m**n*) space is probably a bad idea.
- A simple improvement uses O(*m* + *n*) space, but still not the best solution.
- Could you devise a constant space solution?



### Algorithm

Way1: Use two set variable to store the row and column index to be replaced by 0 respectively.

* Use two set variables row, col to store the index

  ```
  iterate the matrix, once encountering 0 at matrix[i][j], put i into row and j into col.
  ```

* Replace columns and rows by 0

  ```
  for each r in row: matrix[r][j] = 0 for j = [0, len(matrix)[0]-1]
  for each c in col: matrix[i][c] = 0 for i = [0, len(matrix)-1]
  ```

* Complexity Analysis

  * Time: O(m*n)
  * Space: O(m+n)

Way2: Separate the marking and replacing steps and reduce space consumption.

* Iterate the matrix, once encountering 0 at a position, the the 1st element of the row and col to 0 as a mark.

  ```
  e.g. matrix[1][2] = 0 ==> matrix[0][2] = 0 & matrix[1][0] = 0 for marking
  ```

  * One special case need to pay attention to is 0 in the 1st row or column, as it may result in indistinguishable meaning of 0 in 1st row, 1st column.

    ```
    e.g. matrix[1][0] = 0 ==> matrix[1][0] = 0 & matrix[0][0] = 0 # 1st col = 0
    	   matrix[0][1] = 0 ==> matrix[0][0] = 0 & matrix[0][1] = 0 # 1st row = 0
    	   matrix[0][0] = 0 ==> matrix[0][0] = 0										# 1st row, 1st col = 0
    ```

    Thus we use a separate variable col to represent the status of 1st column and use `matrix[0][0]`to represent the status of the 1st row

* Once finish the marking of rows and columns, we update corresponding elements to 0

  * We need to process 2nd - last rows and 2nd - last columns first before processing 1st row and 1st column as update 1st row and 1st column first we influence our results.
  * Process 1st row then 1st column, as when replace 1st column, the 1st element `matrix[0][0]`would be set to 0 no matter it is 0 or not before. When process 1st column first, it may influence 1st row.

* Complexity Analysis

  * Time: O(m*n)
  * Space: O(1)



### Code

```python
class Solution:
    def setZeroes(self, matrix: List[List[int]]) -> None:
        """
        Do not return anything, modify matrix in-place instead.
        """
        # O(m*n) time, O(m+n) space
        row, col = set(), set()
        for i in range(len(matrix)):
            for j in range(len(matrix[0])):
                if matrix[i][j] == 0: 
                    row.add(i)
                    col.add(j)
        for i in row:
            for j in range(len(matrix[0])):
                matrix[i][j] = 0
        for j in col:
            for i in range(len(matrix)):
                matrix[i][j] = 0
```

```python
class Solution:
    def setZeroes(self, matrix: List[List[int]]) -> None:
        """
        Do not return anything, modify matrix in-place instead.
        """
        # O(m*n) time, O(1) space
        col = 1
        for i in range(len(matrix)):
            for j in range(len(matrix[0])):
                if matrix[i][j] == 0:
                    if j == 0:
                        matrix[i][0] = 0
                        col = 0
                    else:
                        matrix[0][j] = 0
                        matrix[i][0] = 0
        for i in range(1,len(matrix)):
            if matrix[i][0] == 0: matrix[i] = [0] * len(matrix[0])
        for j in range(1,len(matrix[0])):
            if matrix[0][j] == 0:
                for i in range(len(matrix)): matrix[i][j] = 0
        if matrix[0][0] == 0: matrix[0] = [0] * len(matrix[0])
        if col == 0:
            for i in range(len(matrix)): matrix[i][0] = 0
```

