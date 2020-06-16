### [368. Largest Divisible Subset](https://leetcode.com/problems/largest-divisible-subset/)
Author: Ruizhe Li  
Date: 06/15/2020

#### Solution & Code
```python
class Solution:
  def largestDivisibleSubset(self, nums: List[int]) -> List[int]:
    """Find the largest divisible subset

    Given a set of distinct positive integers, find the largest 
    subset such that every pair (Si, Sj) of elements in this subset 
    satisfies:
    Si % Sj = 0 or Sj % Si = 0.
    If there are multiple solutions, return any subset is fine.

    Args:
      nums (List[int]): A list of distinct positive integers.

    Returns:
      List[int]: The largest divisible subset.
    """

    def EDS(i):
      """Recursive helper function.


      The recursive helper function to fill in the dynamic 
      programming table. It iterates through the list that 
      smaller than current element nums[i], if it is divisible
      by nums[i], then nums[i] could be added to the end of 
      the subset. We find the maximum subset and append nums[i]
      to the end of it.

      Args:
        i (int): The index of the current element.

      Returns:
        List[int]: The largest divisible subset ended with nums[i].
      """

      # If it is memorized, just return the value.
      if i in memo:
        return memo[i]
  
      # Initialization
      tail = nums[i]
      maxSubset = []
      
      # For each element nums[p] smaller than nums[i],
      # if nums[i] is divisible by nums[p], 
      # find the largest subset ends with nums[p].
      # Find the largest such subset.
      for p in range(0,i):
        if tail % nums[p] == 0:
          subset = EDS(p)
          if len(maxSubset) < len(subset):
            maxSubset = subset

      maxSubset = maxSubset.copy() # Avoid operating on original list
      maxSubset.append(tail) # Append nums[i] to the largest subset found.
      
      memo[i] = maxSubset # Memorize the result
      return maxSubset
    
    if not nums:
      return []
    
    nums.sort()
    memo = {}
    
    return max([EDS(i) for i in range(len(nums))], key=len)
```