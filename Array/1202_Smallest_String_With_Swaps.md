# 1202. Smallest String With Swaps

2020/06/11 ZLY

### Problem Description

You are given a string `s`, and an array of pairs of indices in the string `pairs` where `pairs[i] = [a, b]` indicates 2 indices(0-indexed) of the string.

You can swap the characters at any pair of indices in the given `pairs` **any number of times**.

Return the lexicographically smallest string that `s` can be changed to after using the swaps.



### Algorithm

We use Union Find Algorithm to solve this problem.

Since the pairs can link the characters in the string, we can consider the linked characters as a set. Therefore, firstly for every pair that can swap, we union them to a set. Then we sort the sets. Finally, we put the characters back one by one.

To save time, we use prefix records to continuously update the number of odd occurrences.



### Code

```python
def smallestStringWithSwaps(self, s: str, pairs: List[List[int]]) -> str:
    tmp = list(range(len(s)))
    # classify each index to a 'root' index that represent the set
    def find(x):
        if x != tmp[x]:
            tmp[x] = find(tmp[x])
        return tmp[x]
    #Union Sets
    for i,j in pairs:
        px, py = find(i),find(j)
        if px != py:
            tmp[px] = py
    mem = collections.defaultdict(list)
    # put characters into the sets
    for i,v in enumerate(tmp):
        mem[find(v)].append(s[i])
    # sort the characters in each set
    for k in mem:
        mem[k].sort(reverse=True)
    result = []
    # put characters back
    for i in range(len(s)):
        result.append(mem[find(i)].pop())
    return "".join(result)
```