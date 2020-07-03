# 1409. Queries on a Permutation With Key

2020/07/02 ZLY

### Problem Description

Given the array `queries` of positive integers between `1` and `m`, you have to process all `queries[i]` (from `i=0` to `i=queries.length-1`) according to the following rules:

- In the beginning, you have the permutation `P=[1,2,3,...,m]`.
- For the current `i`, find the position of `queries[i]` in the permutation `P` (**indexing from 0**) and then move this at the beginning of the permutation `P.` Notice that the position of `queries[i]` in `P` is the result for `queries[i]`.

Return an array containing the result for the given `queries`.

 


### Algorithm

We can just use code to simulate the process.



### Code

```python
def processQueries(self, queries: List[int], m: int) -> List[int]:
    p = [x for x in range(1,m+1)]
    result = []
    for x in queries:
        tmp = p.index(x)
        num = p[tmp]
        result.append(tmp)
        p.remove(p[tmp])
        p.insert(0,num)
    return result
```

