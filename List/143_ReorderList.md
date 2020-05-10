### 143. Reorder List
LC link: https://leetcode.com/problems/reorder-list/  
5/10/2020 Ruizhe Li
My Code (Colab): https://colab.research.google.com/drive/1zwh7pppur0pIoEgi3mNOI3cRV9GBBZ0E?usp=sharing

#### Solution
Solve with three steps:
1. Find the middle point and split the list to two halves `lst1` and `lst2`.
1. Reverse the second half `lst2` $\rightarrow$ `reversedLst2`
1. Merge `lst1` and `reversedLst2`

Takeaway:
* Pay attention to corner cases like [ ] and [1]