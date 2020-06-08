# 1146. Snapshot Array

2020/06/08 ZLY

### Problem Description

Implement a SnapshotArray that supports the following interface:

- `SnapshotArray(int length)` initializes an array-like data structure with the given length. **Initially, each element equals 0**.
- `void set(index, val)` sets the element at the given `index` to be equal to `val`.
- `int snap()` takes a snapshot of the array and returns the `snap_id`: the total number of times we called `snap()` minus `1`.
- `int get(index, snap_id)` returns the value at the given `index`, at the time we took the snapshot with the given `snap_id`



### Algorithm

Every time we snap, we just copy the record of last snap, and we only update the value when the `set` function is called.

If a number needs to be smaller, we just change it to `the smaller value of its neighbors - 1`.

In the end, we can just calculate the difference between the new list and the original list, which is exactly the number of moves.



### Code

```python
class SnapshotArray:
    def __init__(self, length: int):
        self.array = [0]*length
        self.history = {}
        self.snap_id = -1
        self.history[self.snap_id] = {}

    def set(self, index: int, val: int) -> None:
        self.history[self.snap_id][index] = val

    def snap(self) -> int:
        import copy
        self.snap_id += 1
        self.history[self.snap_id] = copy.deepcopy(self.history[self.snap_id-1])
        return self.snap_id

    def get(self, index: int, snap_id: int) -> int:
        snap_id -= 1
        if index in self.history[snap_id]:
            return self.history[snap_id][index]
        else:
            return 0


# Your SnapshotArray object will be instantiated and called as such:
# obj = SnapshotArray(length)
# obj.set(index,val)
# param_2 = obj.snap()
# param_3 = obj.get(index,snap_id)
```