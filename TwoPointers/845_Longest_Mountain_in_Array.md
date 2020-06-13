# 845. Longest Mountain in Array

2020/06/13 ZTH

### Problem Description

Let's call any (contiguous) subarray B (of A) a *mountain* if the following properties hold:

- `B.length >= 3`
- There exists some `0 < i < B.length - 1` such that `B[0] < B[1] < ... B[i-1] < B[i] > B[i+1] > ... > B[B.length - 1]`

(Note that B could be any subarray of A, including the entire array A.)

Given an array `A` of integers, return the length of the longest *mountain*. 

Return `0` if there is no mountain.

**Example 1:**

```
Input: [2,1,4,7,3,2,5]
Output: 5
Explanation: The largest mountain is [1,4,7,3,2] which has length 5.
```



### Algorithm

* up variable: record whether exist increase part
* down variable: record whether first increase and then decrease (only could be 1 if up already be 1)
* left variable: current mountain start position, next mountain start = current end
* Procedure
  * If A[i] < A[i-1]
    * set up = 1
    * if down == 1 already: finish one mountain, set left = current position - 1, update maximum mountain length, reset down to 0 (not reset up)
  * If A[i] > A[i-1]
    * if up == 0: left += 1, moves to the right
    * if up == 1: set down = 1
  * If A[i] == A[i-1]
    * if up == 1 
      * if down == 1: one mountain exists and finished, set left = current position, update maximum mountain length
      * reset both up and down to 0 no matter down == 0 or 1
    * if up == 0
      * move the left to the right
* Complexity
  * O(N) time
  * O(1) space



### Code

```python
class Solution:
    def longestMountain(self, A: List[int]) -> int:
        if len(A) < 3: return 0
        up, down, left, ans, i = 0, 0, 0, 0, 1
        while i < len(A):
            if A[i] > A[i-1]: 
                if down == 1:
                    down = 0
                    ans = max(ans, i - left)
                    left = i - 1
                else: up = 1
            elif A[i] < A[i-1]:
                if up == 0: left += 1
                else: down = 1
            else:
                if up == 1:
                    if down == 1: 
                        ans = max(ans, i - left)
                    down = up = 0
                    left = i
                else: left += 1
            i += 1
        if down == 1: ans = max(ans, i-left)
        return ans
                
            
            
        
```

