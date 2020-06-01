# 1031. Maximum Sum of Two Non-Overlapping Subarrays

2020/05/31 ZLY

2020/06/01 ZLY

### Problem Description

Given an array `A` of non-negative integers, return the maximum sum of elements in two non-overlapping (contiguous) subarrays, which have lengths `L` and `M`. (For clarification, the `L`-length subarray could occur before or after the `M`-length subarray.)

Formally, return the largest `V` for which `V = (A[i] + A[i+1] + ... + A[i+L-1]) + (A[j] + A[j+1] + ... + A[j+M-1])` and either:

- `0 <= i < i + L - 1 < j < j + M - 1 < A.length`, **or**
- `0 <= j < j + M - 1 < i < i + L - 1 < A.length`.



### Algorithm 1

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



### Algorithm 2

- Dynamic Programming

  Let's consider the case when L is after M. Let `dpm[i]` represent the max value of M-length subarray among the first `i` numbers. And we have `dpm[i] = max(dpm[i-1],sum[i]-sum[i-M])`. That is, we either select the last M numbers, or we don't select the last number and use the max value from the previous `i-1` numbers. After dealing with dynamic programming, we assume the L-length subarray with max value ends at index `i`, then we just need to find the max-value subarray in the range of `0` to `i-L`, which is just the value of `dpm[i-L]` we get before.



### Code

```python
def maxSumTwoNoOverlap(self, A: List[int], L: int, M: int) -> int:
    dpl = [0]*1001
    dpm = [0]*1001
    sum = [0]*1001
    for i in range(len(A)):
        sum[i+1] = sum[i]+A[i]
    lmax = mmax = result = 0
    for i in range(L+M,len(A)+1):
        lmax = max(lmax,sum[i-M]-sum[i-M-L])
        mmax = max(mmax,sum[i-L]-sum[i-M-L])
        result = max(result,lmax+sum[i]-sum[i-M])
        result = max(result,mmax+sum[i]-sum[i-L])
    return result
```

