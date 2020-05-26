# 978. Longest Turbulent Subarray

2020/05/26 ZLY

### Problem Description

A subarray `A[i], A[i+1], ..., A[j]` of `A` is said to be *turbulent* if and only if:

- For `i <= k < j`, `A[k] > A[k+1]` when `k` is odd, and `A[k] < A[k+1]` when `k` is even;
- **OR**, for `i <= k < j`, `A[k] > A[k+1]` when `k` is even, and `A[k] < A[k+1]` when `k` is odd.

That is, the subarray is turbulent if the comparison sign flips between each adjacent pair of elements in the subarray.

Return the **length** of a maximum size turbulent subarray of A.



### Algorithm

We can use dynamic programming to calculate the longest turbulent substring that ends at each index. We set the start index to be `0` at first. For index `0`, the result is obviously `1`. Continuously, if the following string follows the turbulent rule, the result keep increasing. And if at some index, the turbulent rule is broken, then we set the start index to be this new one. We do this until we reach the end of the list.

* Note when the list is empty or has only one element.

### Code

```python
def maxTurbulenceSize(self, A: List[int]) -> int:
    if len(A)<=1:
        return len(A)
    result = 1
    start = 0
    for i in range(1,len(A)):
        tmp = A[i-1]-A[i]
        if tmp==0:
            start = i
        else:
            if i==len(A)-1 or tmp*(A[i]-A[i+1])>=0:
                result = max(result,i-start+1)
                start = i
    return result
        
```