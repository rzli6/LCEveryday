# 1344. Angle Between Hands of a Clock

2020/05/21 ZLY

### Problem Description

Given two numbers, `hour` and `minutes`. Return the smaller angle (in degrees) formed between the `hour` and the `minute` hand.



### Algorithm

The short hand walks by 30 degree every hour and 0.5 degree every minute. We can then use this to first calculate the degree of the short hand. And as the speed of the long hand is 12 times of the short hand. We can get the degree of the long hand by simply multiplying it by 12. Finally, we substract the degree of long hand by that of short hand to get the angle between them. (to return the smaller angle, we just mod 360 and return the small one between `angle` and `360-angle`)

Once we are done with all the nodes in the original linked list, we just need to join the `small` and `large` linked lists.

At first, we will add an auxiliary "dummy" node, which points to the list head. It can be used to deal with some corner cases such as a list with only one node, or removing the head of the list.

For the two pointers, the first pointer starts from the n+1 node and the second pointer starts from the beginning (the dummy node). And they all step by 1 each time until the first pointer points to `None`. That is, we always maintain n-nodes apart between these two pointers. And when the proceeding stops, we can just let `second.next` to point to `second.next.next`.

### Code

```python
def angleClock(self, hour: int, minutes: int) -> float:
    hour = hour%12
    short_degree = hour*30 + minutes*0.5
    long_degree = short_degree*12
    degree = (long_degree-short_degree)%360
    return min(degree,360-degree)
```