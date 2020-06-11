### [763. Partition Labels](https://leetcode.com/problems/partition-labels/)
Author: Ruizhe Li  
Date: 06/11/2020

#### Solution:
This is a greedy algorithm. We always keep the right most pointer of a section. Whenever we reach a point where the last position of the current element is the current position, we end this section.

#### Code:
```python
class Solution:
    def partitionLabels(self, S: str) -> List[int]:
        """Partition Labels

        A string S of lowercase English letters is given. We want to partition this string into 
        as many parts as possible so that each letter appears in at most one part, and return a 
        list of integers representing the size of these parts.
        
        Args:
            S (str): Input string. All chars are in lower case.
            
        Returns:
            List[int]:  a list of integers representing the size of these parts.
        
        """

        # Dictionary storing the last appearence of a char.
        last = {c: i for i, c in enumerate(S)} 

        # j (int): right boundary of the current section.
        # anchor (int): left boundary of the current section.
        j = anchor = 0
        
        ans = []
        for i, c in enumerate(S):
            j = max(j, last[c])

            # End the list if we the current position equals to the 
            # right boundary of the current section.
            if i == j:
                ans.append(i - anchor + 1)
                anchor = i + 1
                     
        return ans
```