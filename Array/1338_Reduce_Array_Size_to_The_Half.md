# 1338. Reduce Array Size to The Half

2020/06/23 ZLY

### Problem Description

Given an array `arr`. You can choose a set of integers and remove all the occurrences of these integers in the array.

Return *the minimum size of the set* so that **at least** half of the integers of the array are removed.




### Algorithm

First, we count the occurences of each number and store the number of occurences in a list. Then we sort the list from large to small. Finally, we just add the number in the list one by one until we reach 1/2 of the total length of the original array.



### Code

```python
def minSetSize(self, arr: List[int]) -> int:
    total = len(arr)
    occur = []
    arr.sort()
    count = 1
    for i in range(1,total):
        if arr[i] != arr[i-1]:
            occur.append(count)
            count = 1
        else:
            count += 1
    occur.append(count)
    occur.sort(reverse=True)
    result = 0
    size = 0
    for i in range(len(occur)):
        size += occur[i]
        result += 1
        if size >= total//2:
            return result
```