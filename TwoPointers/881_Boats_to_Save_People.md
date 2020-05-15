# 881. Boats to Save People

2020/05/15 ZTH

### Problem Description

The `i`-th person has weight `people[i]`, and each boat can carry a maximum weight of `limit`.

Each boat carries at most 2 people at the same time, provided the sum of the weight of those people is at most `limit`.

Return the minimum number of boats to carry every given person. (It is guaranteed each person can be carried by a boat.)



e.g.

```
Input: people = [1,2], limit = 3
Output: 1
Explanation: 1 boat (1, 2)
```



### Algorithm 

Greedy Algorithm

* Sort the list

* See whether the heaviest one could be carried with the lightest one.

  * if no, the heaviest itself must need a boat

  * if yes, we could carry the two together

    * no need to carry a more heavier one the the lightest with the heaviest as the boat could at most carry 2 people, if the heaviest could match one person, all other people could mathc with this one. Thus, we could simply match heaviest with lightest.

      

### Code

```python
class Solution:
    def numRescueBoats(self, people: List[int], limit: int) -> int:
        # based on the heaviest one
        # each time ans is added with one for the heaviest person
        # if at the same time, we could match the lightest person
        # match the two togther and update the index
        # else, only update the heaviest index
        people.sort()
        left, right, ans = 0, len(people) - 1, 0
        while left <= right:
            ans += 1
            if people[left] + people[right] <= limit:
                left += 1
            right -= 1
        return ans
        
```

