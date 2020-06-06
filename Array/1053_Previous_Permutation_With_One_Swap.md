# 1053. Previous Permutation With One Swap

2020/06/05 ZLY

### Problem Description

Given an array `A` of positive integers (not necessarily distinct), return the lexicographically largest permutation that is smaller than `A`, that can be **made with one swap** (A *swap* exchanges the positions of two numbers `A[i]` and `A[j]`). If it cannot be done, then return the same array.



### Algorithm

We search backward until we find the first number that is not decreasing (or equal). Since if it keeps decreasing, it means that it is already the smallest permutation. For example, for `1 5 2 3 4`, we will find `5`, indicating that `5` is bound to be swapped.

Then we start over from the end and search backward, we find the first number that is smaller than 5. (Since they are decreasing, therefore the first one we find is the largest number that is smaller than 5.)



### Code

```python
def prevPermOpt1(self, A: List[int]) -> List[int]:
    if sorted(A) == A:
        return A
    for i in range(len(A)-1,-1,-1):
        if A[i-1]>A[i]:
            break
    for j in range(len(A)-1,i-1,-1):
        if A[j]<A[i-1] and A[j]!= A[j-1]:
            break
    A[i-1],A[j] = A[j],A[i-1]
    return A
```