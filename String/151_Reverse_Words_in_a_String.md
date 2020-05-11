### 151. Reverse Words in a String
LC link: https://leetcode.com/problems/reverse-words-in-a-string/  
Code: https://colab.research.google.com/drive/1zwh7pppur0pIoEgi3mNOI3cRV9GBBZ0E?usp=sharing  
Author: Ruizhe Li  
Date: 05/10/2020

This question is so trivial for python users that it can be solved in one line.

#### Code:
```python
class Solution:
  def reverseWords(self, s: str) -> str: 
    return ' '.join(s.split()[::-1])
```