# 179. Largest Number

2020/07/04 ZTH

### Problem Description

Given a list of non negative integers, arrange them such that they form the largest number.

**Example 1:**

```
Input: [10,2]
Output: "210"
```

**Example 2:**

```
Input: [3,30,34,5,9]
Output: "9534330"
```

**Note:** The result may be very large, so you need to return a string instead of an integer.



### Algorithm

Bubble Sort

* First convert each element in the given input into string and get new list s.

* For each item pair (s[i], s[j]]), we check the order by comparing s[i] + s[j] with s[j] + s[i] and maintain them in descending order.

  ```
  for i in [0, len(s)-2]:
  	for j in [i+1, len(s)-1]:
  		if s[j] + s[i] > s[i] + s[j]: swap s[i]
  	s[i] fixed
  ```

* Complexity Analysis

  * Time: O(n^2 * a), where n is number of elements in s and a is the average string length
  * Space: O(n * a) for the string list

* Special Case:

  * when all elements start with 0 ==> all elements are 0, the output should be 0 not 000....



### Code

```python
class Solution:
    def largestNumber(self, nums: List[int]) -> str:
        s = [str(e) for e in nums]
        for i in range(len(s)-1):
            for j in range(i+1, len(s)):
                if s[i] + s[j] < s[j] + s[i]: s[i], s[j] = s[j], s[i]
        return str(int(''.join(s)))
```

