### 901. Online Stock Span
Link: https://leetcode.com/problems/online-stock-span/  
Code: https://colab.research.google.com/drive/1zwh7pppur0pIoEgi3mNOI3cRV9GBBZ0E?usp=sharing  
Author: Ruizhe Li  
Date: 05/20/2020  

#### Solution:
Using a stack to maintain a decreasing sorted array.

#### Code:
```python
# Solution
class StockSpanner:

    def __init__(self):
        self.idx = -1
        self.stk = [(-1, 1e9)]
        
    def next(self, price: int) -> int:
        self.idx += 1
        while self.stk[-1][1] <= price:
            self.stk.pop()
        self.stk.append((self.idx,price))
        return self.stk[-1][0]-self.stk[-2][0]


# Your StockSpanner object will be instantiated and called as such:
# obj = StockSpanner()
# param_1 = obj.next(price)
```