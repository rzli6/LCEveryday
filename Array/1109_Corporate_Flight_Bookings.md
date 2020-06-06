# 1109. Corporate Flight Bookings

2020/06/06 ZLY

### Problem Description

There are `n` flights, and they are labeled from `1` to `n`.

We have a list of flight bookings. The `i`-th booking `bookings[i] = [i, j, k]` means that we booked `k` seats from flights labeled `i` to `j` inclusive.

Return an array `answer` of length `n`, representing the number of seats booked on each flight in order of their label.



### Algorithm

The bruteforce method will exceed the time limit.

We consider only marking the start and end points. For one record in the bookings `[start,end,num]`, we let `result[start-1]+=num` and `result[end]-=num`. And finally we calculate the prefix sum.

For example, for `bookings = [[1,2,10],[2,3,20],[2,5,25]], n=5`, we initialize an array `result` of length `6` (`5+1`) of zeros. Then for the first record `[1,2,10]`, we make the array to be `[10,0,-10,0,0,0]`, For second record `[2,3,10]`, we make it `[10,20,-10,-20,0,0]`. For the third record `[2,5,25]`, the array becomes `[10,45,-10,-20,0,-25]`. Then we calculate prefix sum by `result[i]+=result[i-1]`. Finally we just return the `result` array without the last index.

Then we start over from the end and search backward, we find the first number that is smaller than 5. (Since they are decreasing, therefore the first one we find is the largest number that is smaller than 5.)



### Code

```python
def corpFlightBookings(self, bookings: List[List[int]], n: int) -> List[int]:
    result = [0]*(n+1)
    for i in range(len(bookings)):
        result[bookings[i][0]-1] += bookings[i][2]
        result[bookings[i][1]] -= bookings[i][2]
    for i in range(1,len(result)):
        result[i] += result[i-1]
    return result[:-1]
```