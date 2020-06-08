### [518. Coin Change 2](https://leetcode.com/problems/coin-change-2/)
Author: Ruizhe Li  
Date: 06/08/2020

#### Solution:
Dynamic Programming

#### Code:
```python
class Solution:
  def change(self, amount: int, coins: List[int], i = 0) -> int:
    # initialize dp array
    dp = [0]*(amount+1)
    dp[0] = 1
    
    # fill in the array
    for coin in coins:
      for x in range(coin, amount+1):
        dp[x] += dp[x-coin]

    return dp[amount]
```