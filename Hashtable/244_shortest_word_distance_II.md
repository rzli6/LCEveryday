### 244. Shortest Word Distance II
LC link: https://leetcode.com/problems/shortest-word-distance-ii/  
Code: https://colab.research.google.com/drive/1zwh7pppur0pIoEgi3mNOI3cRV9GBBZ0E?usp=sharing  
Author: Ruizhe Li  
Date: 05/10/2020

#### Solution:
1. Init: Given a list of words, we form a dictionary positions = \{word: [pos]\}.
1. Shortest: Because the [pos] is sorted, we can perform "merge" operation on lists positions[word1] and positions[word2].

Takeaway: Use the property of sorted arrays.  
Attention: Input list could contain duplicates.

#### Code:
```python
class WordDistance:
  def __init__(self, words: List[str]):
    self.positions = dict()
    
    # initialize the position array
    for i, word in enumerate(words):
      if word not in self.positions:
        self.positions[word] = []
      self.positions[word].append(i)

  def shortest(self, word1: str, word2: str) -> int:
    i, j, res = 0, 0, 1e9
    # merge operation O(m+n), where m and n are length of two lists
    while i < len(self.positions[word1]) and j < len(self.positions[word2]):
      res = min(res, abs(self.positions[word1][i]-self.positions[word2][j]))
      if self.positions[word1][i] < self.positions[word2][j]:
        i += 1
      else:
        j += 1
    return res
```