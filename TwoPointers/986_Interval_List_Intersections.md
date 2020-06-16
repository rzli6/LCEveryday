# 986. Interval List Intersections

2020/06/15 ZTH

### Problem Description

Given two lists of **closed** intervals, each list of intervals is pairwise disjoint and in sorted order.

Return the intersection of these two interval lists.

*(Formally, a closed interval `[a, b]` (with `a <= b`) denotes the set of real numbers `x` with `a <= x <= b`. The intersection of two closed intervals is a set of real numbers that is either empty, or can be represented as a closed interval. For example, the intersection of [1, 3] and [2, 4] is [2, 3].)*

 

**Example 1:**

**![img](https://assets.leetcode.com/uploads/2019/01/30/interval1.png)**

```
Input: A = [[0,2],[5,10],[13,23],[24,25]], B = [[1,5],[8,12],[15,24],[25,26]]
Output: [[1,2],[5,5],[8,10],[15,23],[24,24],[25,25]]
```

 

**Note:**

1. `0 <= A.length < 1000`
2. `0 <= B.length < 1000`
3. `0 <= A[i].start, A[i].end, B[i].start, B[i].end < 10^9`



### Algorithm

* Initially simply analyzed all cases without considering the regularities among different cases

  * ```
    A[i][0] == B[j][0] ==> [A[i][0], min(A[i][1], B[i][1])], update smaller's index
    ```

  * ```
    A[i][0] < B[j][0]
    	(1) A[i][1] < B[j][0] ==> no intersection, i += 1
    	(2) A[i][1] == B[j][0] ==> [B[j][0], B[j][0]]
    	(3) A[i][1] > B[j][0]
    			- A[i][1] <= B[j][1] ==> [B[j][0], A[i][1]], i += 1
    			- A[i][1] > B[j][1] ==> [B[j]], j += 1
    ```

  * ```
    A[i][0] > B[j][0], similar analysis as previous one
    ```

* If summarize the common pattern

  * ```
    intersection could only be between max(A[i][0], B[j][0]) and min(A[i][1], B[j][1]) when max(A[i][0], B[j][0]) <= min(A[i][1], B[j][1]) 
    ```

  * ```
    pointer update: update smaller one of the end position argmin(A[i][1], B[j][1]) 
    ```

* Complexity Analysis

  * Time: O(A+B), scan two lists
  * Space: O(A+B), store the intersections



### Code

```python
class Solution:
    def intervalIntersection(self, A: List[List[int]], B: List[List[int]]) -> List[List[int]]:
        # O(A+B) time, O(A+B) space 
        p1, p2, ans = 0, 0, []
        
        while p1 < len(A) and p2 < len(B):
            a, b = A[p1], B[p2]
            if a[0] == b[0]:
                ans.append([a[0], min(a[1],b[1])])
                if a[1] >= b[1]: p2 += 1
                else: p1 += 1
            elif a[0] < b[0]:
                if a[1] < b[0]: p1 += 1
                elif a[1] == b[0]:
                    ans.append([b[0],b[0]])
                    p1 += 1
                else:
                    if a[1] <= b[1]: 
                        ans.append([b[0],a[1]])
                        p1 += 1
                    else:
                        ans.append(b)
                        p2 += 1
            else:
                if b[1] < a[0]: p2 += 1
                elif b[1] == a[0]:
                    ans.append([a[0],a[0]])
                    p2 += 1
                else:
                    if b[1] <= a[1]:
                        ans.append([a[0],b[1]])
                        p2 += 1
                    else:
                        ans.append(a)
                        p1 += 1
        return ans
```



```python
class Solution:
    def intervalIntersection(self, A: List[List[int]], B: List[List[int]]) -> List[List[int]]:
        # O(A+B) time, O(A+B) space
        p1, p2, ans = 0, 0, []
        while p1 < len(A) and p2 < len(B):
            a, b = A[p1], B[p2]
            l, r = max(a[0],b[0]), min(a[1],b[1])
            if l <= r: ans.append([l,r])
            if a[1] <= b[1]: p1 += 1
            else: p2 += 1
        return ans
```

