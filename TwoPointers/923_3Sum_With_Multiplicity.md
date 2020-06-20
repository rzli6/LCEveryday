# 923. 3Sum With Multiplicity

2020/06/19 ZTH

### Problem Description

Given an integer array `A`, and an integer `target`, return the number of tuples `i, j, k` such that `i < j < k` and `A[i] + A[j] + A[k] == target`.

**As the answer can be very large, return it modulo `10^9 + 7`**.

 

**Example 1:**

```
Input: A = [1,1,2,2,3,3,4,4,5,5], target = 8
Output: 20
Explanation: 
Enumerating by the values (A[i], A[j], A[k]):
(1, 2, 5) occurs 8 times;
(1, 3, 4) occurs 8 times;
(2, 2, 4) occurs 2 times;
(2, 3, 3) occurs 2 times.
```

**Example 2:**

```
Input: A = [1,1,2,2,2,2], target = 5
Output: 12
Explanation: 
A[i] = 1, A[j] = A[k] = 2 occurs 12 times:
We choose one 1 from [1,1] in 2 ways,
and two 2s from [2,2,2,2] in 6 ways.
```

 

**Note:**

1. `3 <= A.length <= 3000`
2. `0 <= A[i] <= 100`
3. `0 <= target <= 300`



### Algorithm

* As A[i] is within [0, 100], we use this to solve the problem

* Record the occurrence of each A[i] in a dictionary

* There are several situations of the 3Sum, we use variable i, j, k to represent the three values

  * ```
    i != j != k: ans += (dic[i] * dic[j] * dic[k])
    ```

  * ```
    i == j != k: ans += (dic[k] * dic[i] * (dic[i]-1) // 2)
    ```

  * ```
    i != j == k: ans += (dic[i] * dic[k] * (dic[k]-1) // 2)
    ```

  * ```
    i == k != j: ans += (dic[j] * dic[i] * (dic[i]-1) // 2) ==> same as i = j != k as we simply refer the dic for all possible values
    ```

  * ```
    i == j == k: only possible if target % 3 == 0: ans += (dic[i] * (dic[i]-1) * dic[i-2] // (3 * 2))
    ```

* We iterate for each possible i, j, k values respectively

* Complexity Analysis

  * Time: O(N + 100^2)
  * Space: O(100)



### Code

```python
class Solution:
    def threeSumMulti(self, A: List[int], target: int) -> int:
        dic, ans = collections.Counter(A), 0
        # i != j != k
        for i in range(101):
            for j in range(i+1,101):
                k = target - i - j
                if j < k < 101: ans += (dic[i] * dic[j] * dic[k])
        # i == j != k
        for i in range(101):
            k = target - 2 * i
            if i < k < 101: ans += (dic[i] * (dic[i]-1) * dic[k] // 2)
        # i != j == k
        for i in range(101):
            if (target - i) % 2 == 0:
                k = (target - i) // 2
                if i < k < 101: ans += (dic[k] * (dic[k]-1) * dic[i] // 2)
        # i == j == k
        if target % 3 == 0:
            i = target // 3
            if 0 <= i < 101: ans += (dic[i] * (dic[i]-1) * (dic[i]-2) // 6)
        return ans % (1000000007)
```