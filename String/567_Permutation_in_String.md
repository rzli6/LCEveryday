### 567. Permutation in String
Link: https://leetcode.com/problems/permutation-in-string/  
Code: https://colab.research.google.com/drive/1zwh7pppur0pIoEgi3mNOI3cRV9GBBZ0E?usp=sharing  
Author: Ruizhe Li  
Date: 05/18/2020  

#### Solution:
Maintain 2 arrays. One to count the char frequencies in s1, one to count char frequencies in s2. If the two arrays equal to each other, then we found a valid permutation. Otherwise, it is not possible to find a suitable match, return false.

#### Code:
```python
class Solution:
    def checkInclusion(self, s1: str, s2: str) -> bool:
        l, r = 0, 0
        c1 = Counter(s1)
        c2 = Counter()
        target = len(c1)
        cnt = 0
        while r < len(s2):
            c2[s2[r]] += 1
            if c2[s2[r]] == c1[s2[r]]:
                cnt += 1
                if cnt == target:
                    return True
            while c2[s2[r]] > c1[s2[r]]:
                c2[s2[l]] -= 1
                if c2[s2[l]] == 0:
                    cnt -= 1
                l += 1
            r += 1
        return False
```