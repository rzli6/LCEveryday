# 338. Counting Bits

2020/05/23 ZTH

### Problem Description

Given a non negative integer number **num**. For every numbers **i** in the range **0 ≤ i ≤ num** calculate the number of 1's in their binary representation and return them as an array.

**Example 1:**

```
Input: 2
Output: [0,1,1]
```

**Example 2:**

```
Input: 5
Output: [0,1,1,2,1,2]
```

**Follow up:**

- It is very easy to come up with a solution with run time **O(n\*sizeof(integer))**. But can you do it in linear time **O(n)** /possibly in a single pass?
- Space complexity should be **O(n)**.
- Can you do it like a boss? Do it without using any builtin function like **__builtin_popcount** in c++ or in any other language.



### Algorithm

key point: find the relationship between current number and previous

* allocate a variable dp with size n t store # of 1's for each position

```
0,    0,  0   ==> find relationship
01,   1,  1
10,   2,  1
11,   3,  2
100,  4,  1
101,  5,  2
110,  6,  2
111,  7,  3
1000, 8,  1
1001, 9,  2
1010, 10, 2
1011, 11, 3
1100, 12, 2
1101, 13, 3
1110, 14, 3
1111, 15, 4
```

* each odd number

  ```
  dp[i] = dp[i-1] + 1 # i // 2 == 1
  ```

* each even number

  ```
  binary representation of i = binary representation of i // 2 + 0
  e.g. 10 = 1010, 5 = 101
  It is equivalent that for 5 = 2^2 + 2^0, for 10 = 5*2 = (2^2 + 2^0)*2 = 2^3 + 2^1
  
  thus, dp[i] = dp[i//2]
  ```

* Complexity analysis
  * time: O(n) for one scan from 0 to num
  * spaceL O(n) for the dp variable (result)



### Code

```python
class Solution:
    def countBits(self, num: int) -> List[int]:
        dp = [0 for i in range(num + 1)]
        for i in range(1, num + 1):
            if i % 2 == 1: dp[i] = dp[i-1] + 1
            else: dp[i] = dp[i // 2]
        return dp
```

