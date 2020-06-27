# 380. Insert Delete GetRandom O(1)

2020/06/26 ZTH

Design a data structure that supports all following operations in *average* **O(1)** time.

1. `insert(val)`: Inserts an item val to the set if not already present.
2. `remove(val)`: Removes an item val from the set if present.
3. `getRandom`: Returns a random element from current set of elements. Each element must have the **same probability** of being returned.

```python
class RandomizedSet:

    def __init__(self):
        """
        Initialize your data structure here.
        """
        self.ds = set()
    def insert(self, val: int) -> bool:
        """
        Inserts a value to the set. Returns true if the set did not already contain the specified element.
        """
        if val in self.ds: return False
        self.ds.add(val)
        return True
    def remove(self, val: int) -> bool:
        """
        Removes a value from the set. Returns true if the set contained the specified element.
        """
        if val not in self.ds: return False
        self.ds.remove(val)
        return True
    def getRandom(self) -> int:
        """
        Get a random element from the set.
        """
        return random.sample(self.ds,1)[0]


# Your RandomizedSet object will be instantiated and called as such:
# obj = RandomizedSet()
# param_1 = obj.insert(val)
# param_2 = obj.remove(val)
# param_3 = obj.getRandom()
```

