### 886. Possible Bipartition
LC link: https://leetcode.com/problems/possible-bipartition/  
Code: https://colab.research.google.com/drive/1zwh7pppur0pIoEgi3mNOI3cRV9GBBZ0E?usp=sharing  
Author: Ruizhe Li  
Date: 05/28/2020

#### Solution:
It is easy to solve this question using DFS.
* Build a undirected graph according to `dislikes`.
* DFS from any unseen node.
  * If the node has a color already, then check whether its color is same as its parents
    * If same, return False. No Bipartition can be found.
    * Otherwise, continue the algorithm
  * If the node does not have a color, then color it and check all its ajacent nodes
* Return True if all the nodes are colored without any conflict.

Although the algorithm is easy, the Python implementation is quite impressive. I would always recommond you to check the solution and highly voted posts after coming up with your own solution.

#### Code:
```python
from collections import defaultdict
class Solution(object):
  def possibleBipartition(self, N, dislikes):
    graph = defaultdict(list)
    for u, v in dislikes:
      graph[u].append(v)
      graph[v].append(u)
    color = {}
    def dfs(node, c=0):
      if node in color:
        return color[node] == c
      color[node] = c
      return all(dfs(nei, c^1) for nei in graph[node])
    return all(dfs(node) for node in range(1, N+1) if node not in color)
```