# 1375. Bulb Switcher III

2020/06/29 ZLY

### Problem Description

There is a room with `n` bulbs, numbered from `1` to `n`, arranged in a row from left to right. Initially, all the bulbs are turned off.

At moment *k* (for *k* from `0` to `n - 1`), we turn on the `light[k]` bulb. A bulb **change color to blue** only if it is on and all the previous bulbs (to the left) are turned on too.

Return the number of moments in which **all turned on** bulbs **are blue.**




### Algorithm

We record the largest num and the number of lights turned on till now. When the two numbers are equal, it means all lights turned on will become blue, then we add 1 to the result.



### Code

```python
def numTimesAllBlue(self, light: List[int]) -> int:
    if not light:
        return 0
    result = 0
    max_num = 0
    now_num = 0
    for i in range(len(light)):
        now_num += 1
        if light[i] > max_num:
            max_num = light[i]
        if max_num == now_num:
            result += 1
    return result
```

