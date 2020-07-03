# 1395. Count Number of Teams

2020/07/01 ZLY

### Problem Description

There are `n` soldiers standing in a line. Each soldier is assigned a **unique** `rating` value.

You have to form a team of 3 soldiers amongst them under the following rules:

- Choose 3 soldiers with index (`i`, `j`, `k`) with rating (`rating[i]`, `rating[j]`, `rating[k]`).
- A team is valid if: (`rating[i] < rating[j] < rating[k]`) or (`rating[i] > rating[j] > rating[k]`) where (`0 <= i < j < k < n`).

Return the number of teams you can form given the conditions. (soldiers can be part of multiple teams).




### Algorithm

We use two-layer loop to find how many number after it is larger than it for each element and we store it in a dic.

And we run a two-layer loop again to find A < B, then the result can directly add with dic[B]



### Code

```python
def numTeams(self, rating: List[int]) -> int:
    def helper(rating):
        dic = collections.defaultdict(int)
        result = 0
        for i in range(len(rating)):
            for j in range(i+1,len(rating)):
                if rating[j] > rating[i]:
                    dic[i] += 1
        for i in range(len(rating)):
            for j in range(i+1,len(rating)):
                if rating[j] > rating[i]:
                    result += dic[j]
        return result
    return helper(rating) + helper(rating[::-1])
```

