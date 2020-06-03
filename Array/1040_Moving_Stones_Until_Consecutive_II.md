# 1040. Moving Stones Until Consecutive II

2020/06/03 ZLY

### Problem Description

On an **infinite** number line, the position of the i-th stone is given by `stones[i]`. Call a stone an *endpoint stone* if it has the smallest or largest position.

Each turn, you pick up an endpoint stone and move it to an unoccupied position so that it is no longer an endpoint stone.

In particular, if the stones are at say, `stones = [1,2,5]`, you **cannot** move the endpoint stone at position 5, since moving it to any position (such as 0, or 3) will still keep that stone as an endpoint stone.

The game ends when you cannot make any more moves, ie. the stones are in consecutive positions.

When the game ends, what is the minimum and maximum number of moves that you could have made? Return the answer as an length 2 array: `answer = [minimum_moves, maximum_moves]`



### Algorithm

We first sort the `stones` so that the stones are lined in sequence.

For the max value, there are two conditions: 1) We move the stones to the rightmost possible. So we should first move the first stone (sorted) to after the second stone. Then all spaces between stones can be used. So in this case, the number of moves is all spaces between stones excluding the space between the `stones[0]` and `stones[1]`. 2) We can also move the stones to the leftmost possible. Similar to the first case now the number of moves is all spaces between stones excluding the space between `stones[-1]` and `stones[-2]`. And we choose the larger value to be the max number of moves.

For the min value, We can use brute force to search through all possible final ranges of the stones since they will be consecutive at the end. For example, for case: `2 3 4 5 10`, we need 2 moves; for case: `2 3 4 5 10 11`, we also need 2 moves; for case: `2 3 4 5 7 20`, we only need 1 move.

Then we can scan through the list `A`, use `maxval` and `maxindex` to record the `A[i]` and `i`, which makes the largest 

`A[i]+i` till now.

### Code

```python
def numMovesStonesII(self, stones: List[int]) -> List[int]:
    stones.sort()
    n = len(stones)
    spaces = stones[-1]-stones[0]-1-(n-2)
    result = []
    # min value
    l = 0
    minstep = n
    for r in range(n):
        while stones[r]-stones[l]+1>n:
            l+=1
        num = r-l+1
        if num==n-1 and stones[r]-stones[l]==n-2:
            minstep = min(minstep,2)
        else:
            minstep = min(minstep,n-num)
    result.append(minstep)
    # max value
    # move to the rightmost
    steps1 = spaces - (stones[1]-stones[0]-1)
    # move to the leftmost
    steps2 = spaces - (stones[-1]-stones[-2]-1)
    result.append(max(steps1,steps2))
    return result
```