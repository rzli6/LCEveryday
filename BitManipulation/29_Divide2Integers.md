# 29.  Divide Two Integers  
Author: 老刘

## Problem
Given two integers **dividend** and **divisor**, divide two integers without using multiplication, division and mod operator.

Return the quotient after dividing dividend by **divisor**.

The integer division should truncate toward zero, which means losing its fractional part. For example, **truncate(8.345) = 8** and **truncate(-2.7335) = -2**.

## Better Answer
It's stupid to use minus and add to compute the result.  
Good resource:  
[Bitwise operation Source](https://blog.csdn.net/xiaochunyong/article/details/7748713)  

Good answer:  
```
public class Solution {
    public int divide(int dividend, int divisor) {
		if(dividend==Integer.MIN_VALUE && divisor==-1) return Integer.MAX_VALUE;
        if(dividend > 0 && divisor > 0) return divideHelper(-dividend, -divisor);
        else if(dividend > 0) return -divideHelper(-dividend,divisor);
        else if(divisor > 0) return -divideHelper(dividend,-divisor);
        else return divideHelper(dividend, divisor);
    }
    
    private int divideHelper(int dividend, int divisor){
        // base case
        if(divisor < dividend) return 0;
        // get highest digit of divisor
        int cur = 0, res = 0;
        while((divisor << cur) >= dividend && divisor << cur < 0 && cur < 31) cur++;
        res = dividend - (divisor << cur-1);
        if(res > divisor) return 1 << cur-1;
        return (1 << cur-1)+divide(res, divisor);
    }
}
```