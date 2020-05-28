# 1011. Capacity To Ship Package Within D Days

2020/05/28 ZLY

### Problem Description

A conveyor belt has packages that must be shipped from one port to another within `D` days.

The `i`-th package on the conveyor belt has a weight of `weights[i]`. Each day, we load the ship with packages on the conveyor belt (in the order given by `weights`). We may not load more weight than the maximum weight capacity of the ship.

Return the least weight capacity of the ship that will result in all the packages on the conveyor belt being shipped within `D` days.



### Algorithm

We can find out that the lower limit of the final answer is the larger one between `sum(weights)//D` and `max(weights)`. And the upper limit for the final answer is `sum(weights)`. Therefore, we can use binary search between these two limits to find the final answer.



### Code

```python
def shipWithinDays(self, weights: List[int], D: int) -> int:
    high = sum(weights)
    low = max(max(weights),high//D)
    while low<high:
        mid = (high+low)//2
        total = 0
        day = 1
        for weight in weights:
            total += weight
            if total>mid:
                day += 1
                total = weight
        if day>D:
            low = mid+1
        else:
            high = mid
    return low
```