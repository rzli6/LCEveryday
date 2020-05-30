# 1014. Best Sightseeing Pair

2020/05/29 ZLY

### Problem Description

Given an array `A` of positive integers, `A[i]` represents the value of the `i`-th sightseeing spot, and two sightseeing spots `i` and `j` have distance `j - i` between them.

The *score* of a pair (`i < j`) of sightseeing spots is (`A[i] + A[j] + i - j)` : the sum of the values of the sightseeing spots, **minus** the distance between them.

Return the maximum score of a pair of sightseeing spots.



### Algorithm

Since we need `A[i]+A[j]+i-j` to be maximal, then for a fixed `A[j]`, `A[i]+i` should be the maximum (`i<j`).

Then we can scan through the list `A`, use `maxval` and `maxindex` to record the `A[i]` and `i`, which makes the largest 

`A[i]+i` till now.

### Code

```python
def maxScoreSightseeingPair(self, A: List[int]) -> int:
    maxval = A[0]
    maxindex = 0
    result = 0
    for i in range(1,len(A)):
        result = max(result,maxval+A[i]+maxindex-i)
        if A[i]+i > maxval+maxindex:
            maxval = A[i]
            maxindex = i
    return result
```