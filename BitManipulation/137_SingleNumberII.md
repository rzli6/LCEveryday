### 137. Single Number II
LC link: https://leetcode.com/problems/single-number-ii/  
05/10/2020 Ruizhe Li  
My Code (Colab): https://colab.research.google.com/drive/1zwh7pppur0pIoEgi3mNOI3cRV9GBBZ0E?usp=sharing

#### Solution
1. Solution 1:  
As all the numbers are repeated three times except for one number appears only once, we have  
$a_1+a_2+\dots+a_n = (u_1+u_2+\dots+u_k) \times 3 - 2 \times res$  
Where $a_1 \dots a_n$ are elements in the input list, $res$ is the value which appears once, $u_1 \dots u_k$ are the unique values in the input..  
Thus, $res = (\sum_{i=1}^{n} a_{i} - \sum_{i=1}^{k}u_i) / 2$  
We use a hash set to get unique number of the input. Alternatively, we could use hash map which would use more space.

1. Solution 2: bit manipulation  
Citation: https://leetcode.com/problems/single-number-ii/discuss/43295/Detailed-explanation-and-generalization-of-the-bitwise-operation-method-for-single-numbers  
For other numbers repeat $k$ times and a single element appears $p$ time(s)
  1. Initialize $x_1 \dots x_m = 0$, where $m= ceiling(log_2{k})$
  1. Iterate through input array to calculate each counter $x_i$ from most significant to lest significant bits and their mask.
  1. Bitwise OR all the counters to get answer.

Sample template:
```python
for a in nums:
  for i in range(0,m,-1):
    x[i] ^= x[i-1] & x[i-2] & x[0] & a
  mask = getMask(p,x)
  for i in range(0,m):
    x[i] &= mask
  ans = (x[0] | ... | x[m])
```
Please refer to the above link for details.