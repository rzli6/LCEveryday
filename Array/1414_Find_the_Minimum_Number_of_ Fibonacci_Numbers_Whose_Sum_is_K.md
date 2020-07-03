# 1414. Find the Minimum Number of Fibonacci Numbers Whose Sum is K

2020/07/03 ZLY

### Problem Description

Given the number `k`, *return the minimum number of Fibonacci numbers whose sum is equal to* `k`, whether a Fibonacci number could be used multiple times.

The Fibonacci numbers are defined as:

- F1 = 1
- F2 = 1
- Fn = Fn-1 + Fn-2 , for n > 2.

It is guaranteed that for the given constraints we can always find such fibonacci numbers that sum `k`.

 


### Algorithm

First we find two numbers that are the closest to k, (one is larger than k, the other is smaller than k)

Then we keep detracting the largest possible number from k, every time we detract, add 1 to the result.



### Code

```python
def findMinFibonacciNumbers(self, k: int) -> int:
    result = 0
    a = 1
    b = 1
    while b<=k:
        a,b = b,a+b
    while a:
        if a<=k:
            k-=a
            result+=1
        a,b = b-a,a
    return result
```

