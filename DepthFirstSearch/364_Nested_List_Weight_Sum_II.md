### [364. Nested List Weight Sum II](https://leetcode.com/problems/nested-list-weight-sum-ii/)
Author: Ruizhe Li  
Date: 06/02/2020

#### Solution:
Key Idea: Each deeper level means we need to add the element one more time. We do not update *unweight* but keep adding new elements to it. And for each level, we add *unweighted* to the *weighted* answer.

#### Code:
```python
class Solution:
    def depthSumInverse(self, nestedList: List[NestedInteger]) -> int:
        weighted, unweighted = 0, 0
        while nestedList:
            nextLevel = []
            for ni in nestedList:
                if ni.isInteger():
                    unweighted += ni.getInteger()
                else:
                    nextLevel += ni.getList()
            nestedList = nextLevel
            weighted += unweighted
        return weighted
```