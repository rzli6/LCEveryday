# 187. Repeated DNA Sequences

2020/05/27 ZTH

### Problem Description

All DNA is composed of a series of nucleotides abbreviated as A, C, G, and T, for example: "ACGAATTCCG". When studying DNA, it is sometimes useful to identify repeated sequences within the DNA.

Write a function to find all the 10-letter-long sequences (substrings) that occur more than once in a DNA molecule.

**Example:**

```
Input: s = "AAAAACCCCCAAAAACCCCCCAAAAAGGGTTT"

Output: ["AAAAACCCCC", "CCCCCAAAAA"]
```



### Algorithm

* use a dictionary to store the number of occurrence of each 10-letter-long substring

* start from the 1st position (index 0) to the last - 9th position (index last - 10):

  * current substring is 

    * ```
      current = s[i:i+10] for each i or,
      ```

    * ```
      i == 0: current = s[i:i+10] = s[0:10]
      i != 0: current = current[1:] + s[i+9]
      ```

  * each time see a substring, increase one occurence in the dictionary

* In the end, scan the dictionary once and keep these with occurrence larger than 1 as results

* Complexity: 

  * O(N) time
  * O(N) space



### Code

```python
class Solution:
    def findRepeatedDnaSequences(self, s: str) -> List[str]:
        check, ans = {}, []
        for i in range(len(s)-9):
            current = s[i:i+10]
            if current in check: check[current] += 1
            else: check[current] = 1
        for key, value in check.items():
            if value > 1: ans.append(key)
        return ans
```

```python
class Solution:
    def findRepeatedDnaSequences(self, s: str) -> List[str]:
        check, ans = {}, []
        for i in range(len(s)-9):
            if i == 0: current = s[i:i+10]
            else: current = current[1:] + s[i+9]
            if current in check: check[current] += 1
            else: check[current] = 1
        for key, value in check.items():
            if value > 1: ans.append(key)
        return ans
```

