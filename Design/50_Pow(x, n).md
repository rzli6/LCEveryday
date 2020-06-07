# 50. Pow(x, n)

2020/06/07 XDDD

### Problem Description

Implement pow(x, n), which calculates x raised to the power n (xn).

### Algorithm

For n < 0, inverse x and change n to positive. Be careful when n is the MIN_VALUE of int. Convert it to -n will make the wrong value. Cast it to long first.

#### Code:
```Java
class Solution {
    public double myPow(double x, int n) {
        long N = n;
        if(N < 0){
            x = 1 / x;
            N = -N;
        }
        return getPow(x,N);
    }
    
    public double getPow(double x, long n){
        if(n == 0) return 1;
        double res = getPow(x * x, n / 2);
        if(n % 2 == 1){
            res *= x;
        }
        return res;
    }
}
```
