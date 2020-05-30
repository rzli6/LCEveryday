### 973. K Closest Points to Origin
Link: https://leetcode.com/problems/k-closest-points-to-origin/   
Code: https://colab.research.google.com/drive/1zwh7pppur0pIoEgi3mNOI3cRV9GBBZ0E?usp=sharing  
Author: Ruizhe Li  
Date: 05/30/2020  

#### Solution:
Standard quick-sort/quick-selection algorithm which gives O(N) average running time.

#### Code:
```python
class Solution:
  def kClosest(self, points: List[List[int]], K: int) -> List[List[int]]:
    dist = lambda i: points[i][0]**2 + points[i][1]**2
    
    def sort(i,j,K):
      if i >= j:
        return
      
      k = random.randint(i,j)
      points[i], points[k] = points[k], points[i]
      
      mid = partition(i, j)
      if K < mid-i+1:
        sort(i, mid-1, K)
      elif K > mid-i+1:
        sort(mid+1, j, K-(mid-i+1))
    
    def partition(i, j):
      oi = i
      pivot = dist(i)
      i += 1
      
      while True:
        while i < j and dist(i) < pivot:
          i += 1
        while i <= j and dist(j) >= pivot:
          j -= 1
        if i >= j:
          break
        points[i], points[j] = points[j], points[i]
        
      points[oi], points[j] = points[j], points[oi]
      return j
    
    sort(0, len(points)-1, K)
    return points[:K]
```