# 29. Divide Two Integers

Author: LIU Zhuofei  
Date: 2020.6.7  
Rating: 4.5/5.0  

## Problem
Given two integers dividend and divisor, divide two integers without using multiplication, division and mod operator.

Return the quotient after dividing dividend by divisor.

The integer division should truncate toward zero, which means losing its fractional part. For example, truncate(8.345) = 8 and truncate(-2.7335) = -2.

Example:
```
Input: dividend = 10, divisor = 3
Output: 3
Explanation: 10/3 = truncate(3.33333..) = 3.
```

## Idea

### Case of parameters

Is parameter positive or negative? What is the sign of result?

Corner Case: 0? Integer.Max? Integer.Min?

### Binary search

Idea is diviend = a * 2^n * divisor + b * 2^(n-1) * divisor + ...

The way to get a,b... in above equation can be got by binary search.

### Binary Manipulation

to reduce the computation of diviend*2


