# 826. Most Profit Assigning Work

2020/06/12 ZTH

### Problem Description

We have jobs: `difficulty[i]` is the difficulty of the `i`th job, and `profit[i]` is the profit of the `i`th job. 

Now we have some workers. `worker[i]` is the ability of the `i`th worker, which means that this worker can only complete a job with difficulty at most `worker[i]`. 

Every worker can be assigned at most one job, but one job can be completed multiple times.

For example, if 3 people attempt the same job that pays $1, then the total profit will be $3. If a worker cannot complete any job, his profit is $0.

What is the most profit we can make?

**Example 1:**

```
Input: difficulty = [2,4,6,8,10], profit = [10,20,30,40,50], worker = [4,5,6,7]
Output: 100 
Explanation: Workers are assigned jobs of difficulty [4,4,6,6] and they get profit of [20,20,30,30] seperately.
```



### Algorithm

* sort difficulty (with corresponding profit) by ascending order of work difficulty

* sort the workers' ability (worker) in ascending order

* for each worker, the target is to scan from the leftmost of the sorted difficulty list and for each difficulty value smaller or equal than worker's ability, find the maximum profit for the worker

  ```
  current = max(current, profit[i]), where 0 <= i <= index(closest difficult value <= ability)
  ```

* One improvement is that once we sort these lists in ascending order, for worker with larger ability, its value is at least its previous one, we only need to consider index from i (previous end position) to current worker's closet but smaller index instead of starting from 0 each time

* Complexity Analysis

  * Time: O(NlogN + KlogK) for sorting, N = len(difficulty), K = len(worker)
  * Space: O(N)



### Code

```python
class Solution:
    def maxProfitAssignment(self, difficulty: List[int], profit: List[int], worker: List[int]) -> int:
        job, ans, pointer, current = sorted(zip(difficulty, profit)), 0, 0, 0
        for w in sorted(worker):
            while pointer < len(profit) and job[pointer][0] <= w:
                current = max(current, job[pointer][1])
                pointer += 1
            ans += current
        return ans
```

