

# 1352. Product of the Last K Numbers

2020/06/25 ZLY

### Problem Description

Implement the class `ProductOfNumbers` that supports two methods:

1.` add(int num)`

- Adds the number `num` to the back of the current list of numbers.

2.` getProduct(int k)`

- Returns the product of the last `k` numbers in the current list.
- You can assume that always the current list has **at least** `k` numbers.

At any time, the product of any contiguous sequence of numbers will fit into a single 32-bit integer without overflowing.




### Algorithm

If there exists zero in this k numbers, then directly return 0.

If there is no zero, then we can use prefix products to get the result (`prefix(n)//prefix(n-k)`)

And the special case is that when a `0` is added, we can not simply calculate prefix product to `0`, we need to replace it with `1`.

In order to check whether there is `0` in the k numbers, we need an extra variable to update the index of the latest `0`.



### Code

```python
class ProductOfNumbers:

    def __init__(self):
        self.zero_idx = -1
        self.idx = 0
        self.prefix = []

    def add(self, num: int) -> None:
        if num:
            if self.idx:
                self.prefix.append(self.prefix[-1]*num)
            else:
                self.prefix.append(num)
        else:
            self.prefix.append(1)
            self.zero_idx = self.idx
        self.idx += 1
        

    def getProduct(self, k: int) -> int:
        if self.zero_idx >= self.idx-k:
            return 0
        if k == self.idx:
            return self.prefix[-1]
        return self.prefix[-1] // self.prefix[-k-1]


# Your ProductOfNumbers object will be instantiated and called as such:
# obj = ProductOfNumbers()
# obj.add(num)
# param_2 = obj.getProduct(k)
```