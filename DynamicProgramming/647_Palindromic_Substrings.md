# 647. Palindromic Substrings

2020/06/22 ZTH

### Problem Description

Given a string, your task is to count how many palindromic substrings in this string.

The substrings with different start indexes or end indexes are counted as different substrings even they consist of same characters.

**Example 1:**

```
Input: "abc"
Output: 3
Explanation: Three palindromic strings: "a", "b", "c".
```

**Note:**

1. The input string length won't exceed 1000.



### Algorithm

Way1: Dynamic Programming

* We use a dp variable with size nxn to store whether substring within start to end is palindromic

  ```
  e.g. dp[start][end] = True if s[start], s[start+1], ..., s[end] is palindromic
  		 otherwhise False
  ```

* Each time we begin with start == end at each position of input s and expand the start index to left until reach the leftmost position (0 index)

  ```
  e.g. start = end = i for i in range [0, len(s)]
  		 for each situation, update dp[start][end], dp[start-1][end], ..., dp[0][end]
  ```

* We utilize previous results to update dp variable

  ```
  (1) start == end: dp[start][end] = True
  (2) start == end - 1: dp[start][end] = (s[start] == s[end]) # check whether two elements 											 at position start, end are the same
  (3) otherwise (start < end - 1):
  				dp[start][end] = (s[start] == s[end] and dp[start+1][end-1])
  				# check whether two boundary values  the same and  inner substring is palindromic
  ```

* Complexity Analysis:

  * Time: O(n^2) 
  * Space: O(n^2)

Way2: Expand Around Center

* We consider all possible centers for any palindromic substring

  ```
  (1) odd string: the center item
  		e.g. ... aba ... ==> a
  (2) even string: the position in between two center elements
  		e.g. ... a_b ... ==> _ between ab
  ```

  Thus, there are n (n elements) + (n-1) (n-1 in between positions) = 2n-1 possible centers

  ```
  e.g. input: abaab
       centers: a, _, b, _, a, _, a, _, b (9 possible centers)
  ```

* For each possible center, we start from the smallest substring around it and expand in left and right directions

  ```
  e.g. a_b_a_a_b
  		 012345678
  		 abaab
  		 01234
  (1) 2nd 'a' as center: smallest substring is 'a' ==> left = 4 // 2 = 2, right = 2 + 0 = 2
  (2) 1st '_' as center: smallest substring is 'ab' => left = 1 // 2 = 0, right = 0 + 1 = 1
  ```

  * Once figure out the left and right position, check whether s[left] == s[right], if yes, minus left by 1 and add right by 1 until left reaches 0 or right reaches len(s) - 1

* Complexity Analysis:

  * Time: O(n^2)
  * Space: O(n^2)



### Code

```python
class Solution:
    def countSubstrings(self, s: str) -> int:
        # O(n^2) time, O(n^2) space
        dp, ans = [[False for i in range(len(s))] for j in range(len(s))], 0
        for i in range(len(s)):
            start = end = i
            while start >= 0:
                if start == end: dp[start][end] = True
                elif start + 1 == end: dp[start][end] = (s[start] == s[end])
                else: dp[start][end] = (dp[start+1][end-1] and s[start] == s[end])
                if dp[start][end] == True: ans += 1
                start -= 1
        return ans
```

```python
class Solution:
    def countSubstrings(self, s: str) -> int:
        # O(n^2) time, O(1) space
        ans = 0
        for c in range(2*len(s) -1):
            left = c // 2
            right = left + c % 2
            while left >= 0 and right < len(s) and s[left] == s[right]:
                ans += 1
                left -= 1
                right += 1
        return ans
```

