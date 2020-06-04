# 1052. Grumpy Bookstore Owner

2020/06/04 ZLY

### Problem Description

Today, the bookstore owner has a store open for `customers.length` minutes. Every minute, some number of customers (`customers[i]`) enter the store, and all those customers leave after the end of that minute.

On some minutes, the bookstore owner is grumpy. If the bookstore owner is grumpy on the i-th minute, `grumpy[i] = 1`, otherwise `grumpy[i] = 0`. When the bookstore owner is grumpy, the customers of that minute are not satisfied, otherwise they are satisfied.

The bookstore owner knows a secret technique to keep themselves not grumpy for `X` minutes straight, but can only use it once.

Return the maximum number of customers that can be satisfied throughout the day.



### Algorithm

Maximum number of satisfied customers => Total customers - Minimum unsatisfied customers

Minimum unsatisfied customers => Total unsatisfied customers - Maximum unsatisfied customers in X time period

So the aim is to find a X-time period with maximum unsatisfied customers

Here I move the X-length window from left ro right of the array, each time, to calculate the number of unsatisfied customers, and find the minimum among all the results.



### Code

```python
def maxSatisfied(self, customers: List[int], grumpy: List[int], X: int) -> int:
    result = 0
    for i in range(len(customers)):
        result += customers[i]
    if len(grumpy) == X:
        return result
    diff = []
    for i in range(len(customers)):
        diff.append(customers[i]*grumpy[i])
    s = 0
    for i in range(X,len(customers)):
        s += diff[i]
    temp = s
    left = 1
    right = left+X-1
    while right<len(customers):
        temp = temp + diff[left-1]-diff[right]
        if temp<s:
            s = temp
        left += 1
        right += 1
    return result-s
```