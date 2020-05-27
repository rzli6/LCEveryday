# 1007. Minimum Domino Rotations For Equal Row

2020/05/27 ZLY

### Problem Description

In a row of dominoes, `A[i]` and `B[i]` represent the top and bottom halves of the `i`-th domino. (A domino is a tile with two numbers from 1 to 6 - one on each half of the tile.)

We may rotate the `i`-th domino, so that `A[i]` and `B[i]` swap values.

Return the minimum number of rotations so that all the values in `A` are the same, or all the values in `B` are the same.

If it cannot be done, return `-1`.



### Algorithm

We can first find out all the possible final values since the value only ranges from 1 to 6. If there is no possible value, then directly return `-1`.

For all possible values, we calculate the number of rotations needed (the smaller one between rotating A and rotating B). Finally, we return the minimum rotations for all possible values.



### Code

```python
def minDominoRotations(self, A: List[int], B: List[int]) -> int:
    possible_value = []
    for i in range(1,7):
        flag = 1
        for j in range(len(A)):
            if A[j]!=i and B[j]!=i:
                flag = 0
                break
        if flag:
            possible_value.append(i)
    if not len(possible_value):
        return -1
    result_list=[]
    for val in possible_value:
        count1 = 0
        count2 = 0
        for j in range(len(A)):
            if A[j]==val:
                count1 += 1
            if B[j]==val:
                count2 += 1
        result_list.append(min(len(A)-count1,len(A)-count2))
    return min(result_list)
```