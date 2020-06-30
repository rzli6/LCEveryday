# 1386. Cinema Seat Allocation

2020/06/30 ZLY

### Problem Description

![img](https://assets.leetcode.com/uploads/2020/02/14/cinema_seats_1.png)

A cinema has `n` rows of seats, numbered from 1 to `n` and there are ten seats in each row, labelled from 1 to 10 as shown in the figure above.

Given the array `reservedSeats` containing the numbers of seats already reserved, for example, `reservedSeats[i] = [3,8]` means the seat located in row **3** and labelled with **8** is already reserved.

*Return the maximum number of four-person groups you can assign on the cinema seats.* A four-person group occupies four adjacent seats **in one single row**. Seats across an aisle (such as [3,3] and [3,4]) are not considered to be adjacent, but there is an exceptional case on which an aisle split a four-person group, in that case, the aisle split a four-person group in the middle, which means to have two people on each side.




### Algorithm

According to the restrictions, we can know that a row can contain two groups at most. And for one group, it can only has three choices(i.e. 2345, 4567, 6789). Therefore, we can only check the conditions of 23, 45, 67, 89 for each row. And for rows that is not reserved, we directly add 2 to the result.



### Code

```python
def maxNumberOfFamilies(self, n: int, reservedSeats: List[List[int]]) -> int:
    dic = collections.defaultdict(set)
    result = 0
    reservedRow = set()
    for row,seat in reservedSeats:
        dic[row].add(seat)
        reservedRow.add(row)
    for row in reservedRow:
        tt = 2 not in dic[row] and 3 not in dic[row]
        ff = 4 not in dic[row] and 5 not in dic[row]
        ss = 6 not in dic[row] and 7 not in dic[row]
        en = 8 not in dic[row] and 9 not in dic[row]
        if tt and ff and ss and en:
            result += 2
        elif tt and ff:
            result += 1
        elif ff and ss:
            result += 1
        elif ss and en:
            result += 1
    return result + (n-len(reservedRow))*2
```

