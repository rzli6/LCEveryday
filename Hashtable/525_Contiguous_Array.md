### 525. Contiguous Array
Link: https://leetcode.com/problems/contiguous-array/   
Code: https://colab.research.google.com/drive/1zwh7pppur0pIoEgi3mNOI3cRV9GBBZ0E?usp=sharing  
Author: Ruizhe Li  
Date: 05/27/2020  

#### Solution:
Maintain a hashtable to record the difference between number of 1s and number of 0s (#1 - #0). For example, we have an array, [0,0,0,1,0,1,1] , the corresponding difference array is *diff=[-1,-2,-3,-2,-3,-2,-1]*. If diff[i] == diff[j], then there is a continuous sub-array [i+1:j+1] that contains same number of 0s and 1s. We just need to find the longest such array.  
Instead of an extra array recording the difference. We can use a hash map to record the earlist position of each difference in difference records. And update the result on the fly.

#### Code:
```python
class Solution:
  def findMaxLength(self, nums: List[int]) -> int:
    record = {0:-1} # hashtable recording the earlist occurence of a difference value
    cnt, res = 0, 0 # counter, result
    for i, e in enumerate(nums):
      cnt += 2*e-1 # update counter
      if cnt in record:
        res = max(res, i-record[cnt]) # update result
      else:
        record[cnt] = i # set earlist occurance
    return res
```