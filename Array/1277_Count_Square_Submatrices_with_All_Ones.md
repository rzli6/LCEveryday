### 1277. Count Square Submatrices with All Ones
Link: https://leetcode.com/problems/count-square-submatrices-with-all-ones/   
Code: https://colab.research.google.com/drive/1zwh7pppur0pIoEgi3mNOI3cRV9GBBZ0E?usp=sharing  
Author: Ruizhe Li  
Date: 05/26/2020  

#### Solution:
**Dynamic Programming**  
The squre position is represented by the position of its right corner.
* Key Idea: For matrix[i][j] record how many square can be formed with the right corner set at [i][j].  
* It turns out that the number of square can be formed at [i][j] equals to side length of the largest squre can be formed here.  

We use dynamic programming to record this value. If a square of side size n can be formed at [i][j] if and only if a square of side size n-1 can be formed at [i-1][j], [i][j-1], and [i-1][j-1]. Thus, we have the following algorithm.

#### Code:
```python
class Solution:
  def countSquares(self, matrix: List[List[int]]) -> int:
    for i in range(1, len(matrix)):
      # for each row
      for j in range(1, len(matrix[0])):
        # for each entry
        # if the value is 0 at [i][j] then 0 is returned, otherwise
        # the largest squre can be formed is the min of its up, left, left-up ajacent position + 1
        matrix[i][j] *= min(matrix[i-1][j], matrix[i][j-1], matrix[i-1][j-1])+1
    return sum(map(sum, matrix))
```