# 62. Unique Paths

2020/05/17 ZTH

### Problem Description

A robot is located at the top-left corner of a *m* x *n* grid (marked 'Start' in the diagram below).

The robot can only move either down or right at any point in time. The robot is trying to reach the bottom-right corner of the grid (marked 'Finish' in the diagram below).

How many possible unique paths are there?

e.g.

```
Input: m = 3, n = 2
Output: 3
Explanation:
From the top-left corner, there are a total of 3 ways to reach the bottom-right corner:
1. Right -> Right -> Down
2. Right -> Down -> Right
3. Down -> Right -> Right
```



### Algorithm

1. **Way 1 Backtracking** ==> Time Limit Exceeded

   * for the mxn grid, # of possible unique paths includes *m-1 down steps* & *n-1 right steps*
   * the # of possible unique paths of position *m,n* = # of possible paths of position *m-1,n* + # of possible paths of position *m,n-1*
   * the # of possible unique paths when *m=1* or *n=1* is 1 
   * from the last position *m,n* to the beginning  

2. **Way 2 Dynamic Programming** ==> O(*mn*) time, O(*mn*) space

   * start from beginning to the end

   * allocate a *mxn* box to store # of possible unique paths of each position

     * the first row (*m=1*) & first column (*n=1*) are all 1

     * for other positions, iterate the 2d loops and fill elements one by one from the top-left to bottom-right: 

       ``` 
       box[i][j] = box[i-1][j] + box[i][j-1]
       ```

3. **Way 3 Dynamic Programming** ==> O(*mn*) time, O(*n*) space

   * similar as way2, but we only use box with size *n*

   * we regard box stored the last row's result

     * original 2d box

       ```
       box = [1,1,1,1, 1, 1, 1]
       			[1,2,3,4, 5, 6, 7]
       			[1,3,6,10,15,21,28]
       box[i][j] = box[i-1][j] + box[i][j-1] (e.g. 15 = 10 + 5)
       ```

     * updated 1d box

       ```
       1st iteration: box = [1,1,1,1, 1, 1, 1]
       2nd iteration: box = [1,2,3,4, 5, 6, 7] 
       3rd iteration: box = [1,3,6,10,15,21,28]
       box[i] = box[i] + box[i-1] for i in range(1,n)
       ```

   * we iterate the update steps for m times, each time go through the box (size *n*) == iterate once and fill the box (size *mn*)

4. **Way 4 Math** ==> O(*m+n*) time, O(1) space

   * it is a math problem for the number of possible permutations of *(m-1)* down and *(n-1)* right

   * then there are possible unique permutations:
     $$
     (m-1+n-1)!/((m-1)!(n-1)!)
     $$
     

### Code

```python
class Solution:
    def uniquePaths(self, m: int, n: int) -> int:
        # way 1: backtracking ==> Time limit exceeded
        if m == 1 or n == 1: return 1
        else: return self.uniquePaths(m-1, n) + self.uniquePaths(m, n-1)
```

```python
class Solution:
    def uniquePaths(self, m: int, n: int) -> int:
        # way 2: dynamic programming ==> O(m*n) time, O(m*n) space
        box = [[1 for i in range(n)] for j in range(m)]
        for i in range(1,m):
            for j in range(1, n):
                box[i][j] = box[i-1][j] + box[i][j-1]
        return box[-1][-1]
        
```

```python
class Solution:
    def uniquePaths(self, m: int, n: int) -> int:
        # way 3: dynamic programming ==> O(m*n) time, O(n) space
        box = [1 for i in range(n)]
        for i in range(1,m):
            for j in range(1, n):
                box[j] += box[j-1]
        return box[-1]
```

```python
class Solution:
    def uniquePaths(self, m: int, n: int) -> int:
        # way 4: math ==> O(m+n) time, O(1) space
        if m == 1 or n == 1: return 1
        def factorial(x):
            ans = 1
            for i in range(1,x+1):
                ans *= i
            return ans
        return int(factorial(m + n - 2) / (factorial(m - 1) * factorial(n - 1)))
```

