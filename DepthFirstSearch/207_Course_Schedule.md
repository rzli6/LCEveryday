### 207. Course Schedule
LC link: https://leetcode.com/problems/course-schedule/  
Code: https://colab.research.google.com/drive/1zwh7pppur0pIoEgi3mNOI3cRV9GBBZ0E?usp=sharing  
Author: Ruizhe Li  
Date: 05/30/2020

#### Solution:
Standard topological sort (DFS) to detect cycle. It is available as long as there is no cycle in the graph.

#### Code:
```python
class Solution:
  def canFinish(self, numCourses: int, prerequisites: List[List[int]]) -> bool:
    graph = defaultdict(list)
    inNums = [0]*numCourses
    avails = []
    
    for p in prerequisites:
      graph[p[0]].append(p[1])
      inNums[p[1]] += 1
  
    avails = [i for i, num in enumerate(inNums) if num == 0]
    
    while avails:
      course = avails.pop()
      for c in graph[course]:
        inNums[c] -= 1
        if inNums[c] == 0:
          avails.append(c)
        
      return sum(inNums) == 0
```