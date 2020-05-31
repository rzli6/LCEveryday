# 1031. Maximum Sum of Two Non-Overlapping Subarrays

2020/05/31 ZLY

### Problem Description

Given an array `A` of non-negative integers, return the maximum sum of elements in two non-overlapping (contiguous) subarrays, which have lengths `L` and `M`. (For clarification, the `L`-length subarray could occur before or after the `M`-length subarray.)

Formally, return the largest `V` for which `V = (A[i] + A[i+1] + ... + A[i+L-1]) + (A[j] + A[j+1] + ... + A[j+M-1])` and either:

- `0 <= i < i + L - 1 < j < j + M - 1 < A.length`, **or**
- `0 <= j < j + M - 1 < i < i + L - 1 < A.length`.



### Algorithm

- Brute force.

  We use two dictionaries to record all the sum of ` L`-length subarray and `M`-length subarray. Then we consider two conditions: 1) L is before M; 2) L is after M.

Then we can scan through the list `A`, use `maxval` and `maxindex` to record the `A[i]` and `i`, which makes the largest 

`A[i]+i` till now.

### Code

```python
def maxSumTwoNoOverlap(self, A: List[int], L: int, M: int) -> int:
    Ldict = {}
    Mdict = {}
    for i in range(len(A)-L+1):
        if i==0:
            Ldict[i] = sum(A[:L])
        else:
            Ldict[i] = Ldict[i-1]-A[i-1]+A[i+L-1]
    for i in range(len(A)-M+1):
        if i==0:
            Mdict[i] = sum(A[:M])
        else:
            Mdict[i] = Mdict[i-1]-A[i-1]+A[i+M-1]
    result = 0
    for i in range(len(A)-L+1):
        for j in range(i+L,len(A)-M+1):
            result = max(result,Ldict[i]+Mdict[j])
    for i in range(len(A)-M+1):
        for j in range(i+M,len(A)-L+1):
            result = max(result,Ldict[j]+Mdict[i])
    return result
```