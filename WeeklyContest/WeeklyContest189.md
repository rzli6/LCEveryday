### 5412. Number of Students Doing Homework at a Given Time
Difficulty: Easy  
Given two integer arrays `startTime` and `endTime` and given an integer `queryTime`.

The `ith` student started doing their homework at the time `startTime[i]` and finished it at time `endTime[i]`.

Return the number of students doing their homework at time `queryTime`. More formally, return the number of students where `queryTime` lays in the interval `[startTime[i], endTime[i]]` inclusive.

 

**Example 1:**  
```
Input: startTime = [1,2,3], endTime = [3,2,7], queryTime = 4
Output: 1
Explanation: We have 3 students where:
The first student started doing homework at time 1 and finished at time 3 and wasn't doing anything at time 4.
The second student started doing homework at time 2 and finished at time 2 and also wasn't doing anything at time 4.
The third student started doing homework at time 3 and finished at time 7 and was the only student doing homework at time 4.
```

**Example 2:**  
```
Input: startTime = [4], endTime = [4], queryTime = 4
Output: 1
Explanation: The only student was doing their homework at the queryTime.
```

**Example 3:**  
```
Input: startTime = [4], endTime = [4], queryTime = 5
Output: 0
```

**Example 4:**  
```
Input: startTime = [1,1,1,1], endTime = [1,3,2,4], queryTime = 7
Output: 0
```

**Example 5:**  
```
Input: startTime = [9,8,7,6,5,4,3,2,1], endTime = [10,10,10,10,10,10,10,10,10], queryTime = 5
Output: 5
```

**Constraints:** 

* startTime.length == endTime.length
* 1 <= startTime.length <= 100
* 1 <= startTime[i] <= endTime[i] <= 1000
* 1 <= queryTime <= 1000

#### Code:
```python
from typing import List
class Solution:
  def busyStudent(self, startTime: List[int], endTime: List[int], queryTime: int) -> int:
    return sum([1 for s, e in zip(startTime, endTime) if s <= queryTime <= e])
```

### 5413. Rearrange Words in a Sentence
Difficulty: Medium  

Given a sentence text (A sentence is a string of space-separated words) in the following format:  

* First letter is in upper case.
* Each word in text are separated by a single space.  

Your task is to rearrange the words in text such that all words are rearranged in an increasing order of their lengths. If two words have the same length, arrange them in their original order.  

Return the new text following the format shown above.  

**Example 1:**  
```
Input: text = "Leetcode is cool"
Output: "Is cool leetcode"
Explanation: There are 3 words, "Leetcode" of length 8, "is" of length 2 and "cool" of length 4.
Output is ordered by length and the new first word starts with capital letter.
```
**Example 2:**  
```
Input: text = "Keep calm and code on"
Output: "On and keep calm code"
Explanation: Output is ordered as follows:
"On" 2 letters.
"and" 3 letters.
"keep" 4 letters in case of tie order by position in original text.
"calm" 4 letters.
"code" 4 letters.
```

**Example 3:**  
```
Input: text = "To be or not to be"
Output: "To be or to be not"
```

**Constraints:**  

* text begins with a capital letter and then contains lowercase letters and single space between words.
* 1 <= text.length <= 10^5

#### Code:
```python
class Solution:
  def arrangeWords(self, text: str) -> str:
    return ' '.join(sorted(text.split(), key=lambda x: len(x))).lower().capitalize()
```

### 5414. People Whose List of Favorite Companies Is Not a Subset of Another List
Difficulty: Medium  

Given the array `favoriteCompanies` where `favoriteCompanies[i]` is the list of favorites companies for the `ith` person **(indexed from 0)**.  

*Return the indices of people whose list of favorite companies is not a **subset** of any other list of favorites companies.* You must return the indices in increasing order.

 

**Example 1:**  
```
Input: favoriteCompanies = [["leetcode","google","facebook"],["google","microsoft"],["google","facebook"],["google"],["amazon"]]
Output: [0,1,4] 
Explanation: 
Person with index=2 has favoriteCompanies[2]=["google","facebook"] which is a subset of favoriteCompanies[0]=["leetcode","google","facebook"] corresponding to the person with index 0. 
Person with index=3 has favoriteCompanies[3]=["google"] which is a subset of favoriteCompanies[0]=["leetcode","google","facebook"] and favoriteCompanies[1]=["google","microsoft"]. 
Other lists of favorite companies are not a subset of another list, therefore, the answer is [0,1,4].
```
**Example 2:**  
```
Input: favoriteCompanies = [["leetcode","google","facebook"],["leetcode","amazon"],["facebook","google"]]
Output: [0,1] 
Explanation: In this case favoriteCompanies[2]=["facebook","google"] is a subset of favoriteCompanies[0]=["leetcode","google","facebook"], therefore, the answer is [0,1].
```
**Example 3:**  
```
Input: favoriteCompanies = [["leetcode"],["google"],["facebook"],["amazon"]]
Output: [0,1,2,3]
```

**Constraints:**  

* 1 <= favoriteCompanies.length <= 100
* 1 <= favoriteCompanies[i].length <= 500
* 1 <= favoriteCompanies[i][j].length <= 20
* All strings in favoriteCompanies[i] are distinct.
* All lists of favorite companies are distinct, that is, If we sort alphabetically each list then favoriteCompanies[i] != favoriteCompanies[j].
* All strings consist of lowercase English letters only.

#### Code:
```python
class Solution:
  def peopleIndexes(self, favoriteCompanies: List[List[str]]) -> List[int]:
    n = len(favoriteCompanies)
    res = [False] * n
    favoriteCompanies = [set(c) for c in favoriteCompanies]

    for i in range(n):
      for j in range(i):
        if res[i]:
          break
        if not res[j]:
          intersection = favoriteCompanies[j].intersection(favoriteCompanies[i])
          if intersection == favoriteCompanies[i]:
            res[i] = True
          if intersection == favoriteCompanies[j]:
            res[j] = True
    return [i for i in range(len(res)) if not res[i]]
```


### 5415. Maximum Number of Darts Inside of a Circular Dartboard
Difficulty: Hard  

You have a very large square wall and a circular dartboard placed on the wall. You have been challenged to throw darts into the board blindfolded. Darts thrown at the wall are represented as an array of `points` on a 2D plane. 

Return the maximum number of points that are within or lie on any circular dartboard of radius r.

 

**Example 1:**  
```
Input: points = [[-2,0],[2,0],[0,2],[0,-2]], r = 2
Output: 4
Explanation: Circle dartboard with center in (0,0) and radius = 2 contain all points.
```
**Example 2:**
```
Input: points = [[-3,0],[3,0],[2,6],[5,4],[0,9],[7,8]], r = 5
Output: 5
Explanation: Circle dartboard with center in (0,4) and radius = 5 contain all points except the point (7,8).
```
**Example 3:**  
```
Input: points = [[-2,0],[2,0],[0,2],[0,-2]], r = 1
Output: 1
```
**Example 4:**
```
Input: points = [[1,2],[3,5],[1,-1],[2,3],[4,1],[1,3]], r = 2
Output: 4
```

**Constraints:** 

* 1 <= points.length <= 100
* points[i].length == 2
* -10^4 <= points[i][0], points[i][1] <= 10^4
* 1 <= r <= 5000

#### Code:
For details: https://www.geeksforgeeks.org/angular-sweep-maximum-points-can-enclosed-circle-given-radius/
```python
from typing import List
from math import acos, atan2, sqrt

class Solution:
  def pointsInside(self, i, r, n):
    angles = []
    for j in range(n):
      if i != j and self.dist[i][j] <= 2*r:
        A = atan2(points[i][1]-points[j][1],points[i][0]-points[j][0])
        B = acos(self.dist[i][j]/(2*r))
        
        a = A-B
        b = A+B

        angles.append((a, True))
        angles.append((b, False))
    
    angles = sorted(angles, key=lambda p: -p[1])
    angles = sorted(angles, key=lambda p: p[0])

    count = res = 1
    for _, flag in angles:
      if flag:
        count += 1
      else:
        count -= 1
      res = max(res, count)
    
    return res

  def maxPoints(self, points, n, r):
    for i in range(n):
      for j in range(n):
        self.dist[i][j] = self.dist[j][i] = sqrt((points[i][0]-points[j][0])**2+(points[i][1]-points[j][1])**2)
    
    ans = max(self.pointsInside(i,r,n) for i in range(n))
    return ans

  def numPoints(self, points: List[List[int]], r: int) -> int:
    n = len(points)
    self.dist = [[None]*n for _ in range(n)]
    return self.maxPoints(points, n, r)
```