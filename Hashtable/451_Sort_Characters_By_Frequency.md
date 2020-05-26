### 451. Sort Characters By Frequency
Link: https://leetcode.com/problems/sort-characters-by-frequency/   
Code: https://colab.research.google.com/drive/1zwh7pppur0pIoEgi3mNOI3cRV9GBBZ0E?usp=sharing  
Author: Ruizhe Li  
Date: 05/26/2020  

#### Solution:
This problem is rather easy if we make use of `Counter` in Python.  
If we do not want to use the `Counter` class, we can use a dictionary and do bucket sorting instead. 

#### Code:
```python
class Solution:
  def frequencySort(self, s: str) -> str:
    return ''.join([c*n for c, n in Counter(s).most_common()])
```