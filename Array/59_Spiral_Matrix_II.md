# 59. Spiral Matrix II

2020/06/30 ZTH

### Problem Description

Given a positive integer *n*, generate a square matrix filled with elements from 1 to *n*2 in spiral order.

**Example:**

```
Input: 3
Output:
[
 [ 1, 2, 3 ],
 [ 8, 9, 4 ],
 [ 7, 6, 5 ]
]
```

### Algorithm

Use similar way as Spiral Matrix probelm.

* Truncate the process into iterations, where each iteration includes 4 procedures if needed.

  ```
  The 1st iteration
  (1) left -> right  ==> e.g. 1,2,3
  (2) up -> down 		 ==> e.g. 4,5	
  (3) right -> left	 ==> e.g. 6,7
  (4) down -> up 		 ==> e.g. 8
  ```

* For iteration i, the corresponding index is below: (i starts with 0)

  ```
  The i-th iteration, i in [0, (n+1)//2]
  (1) left -> right  ==> ans[i][c], c in [i, n-i-1]
  (2) up -> down 		 ==> ans[r][n-i-1], r in [i+1, n-i-1]	
  (3) right -> left	 ==> ans[n-i-1][c], c in [n-i-1-1, i]
  (4) down -> up 		 ==> ans[r][i], r in [n-i-1-1, i+1]
  
  The iteration times:
  even n (n % 2 == 0): n // 2
  odd n (n % 2 != 0): (n + 1) // 2 
  ==> all n: (n + 1) // 2
  ```

* Complexity Analysis

  * Time: O(n^2)
  * Space: O(n^2)



### Code

```python
class Solution:
    def generateMatrix(self, n: int) -> List[List[int]]:
        ans, val = [[0 for i in range(n)] for j in range(n)], 1
        for i in range((n + 1) // 2):
            for c in range(i, n-i):
                ans[i][c] = val
                val += 1
            for r in range(i+1, n-i):
                ans[r][n-i-1] = val
                val += 1
            for c in range(n-i-1-1, i-1, -1):
                ans[n-i-1][c] = val
                val += 1
            for r in range(n-i-1-1, i, -1):
                ans[r][i] = val
                val += 1
        return ans
```

