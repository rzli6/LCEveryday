# 838. Push Dominoes

2020/06/14 ZTH

### Problem Description

There are `N` dominoes in a line, and we place each domino vertically upright.

In the beginning, we simultaneously push some of the dominoes either to the left or to the right.

![img](https://s3-lc-upload.s3.amazonaws.com/uploads/2018/05/18/domino.png)

After each second, each domino that is falling to the left pushes the adjacent domino on the left.

Similarly, the dominoes falling to the right push their adjacent dominoes standing on the right.

When a vertical domino has dominoes falling on it from both sides, it stays still due to the balance of the forces.

For the purposes of this question, we will consider that a falling domino expends no additional force to a falling or already fallen domino.

Given a string "S" representing the initial state. `S[i] = 'L'`, if the i-th domino has been pushed to the left; `S[i] = 'R'`, if the i-th domino has been pushed to the right; `S[i] = '.'`, if the `i`-th domino has not been pushed.

Return a string representing the final state. 

**Example 1:**

```
Input: ".L.R...LR..L.."
Output: "LL.RR.LLRRLL.."
```

**Example 2:**

```
Input: "RR.L"
Output: "RR.L"
Explanation: The first domino expends no additional force on the second domino.
```

**Note:**

1. `0 <= N <= 10^5`
2. String `dominoes` contains only `'L`', `'R'` and `'.'`



### Algorithm

* The idea of sliding window: the window is bordered by 'L' or 'R' with all center elements '.' or empty. e.g. 'L...R' or 'LR'
* Each time we process one sliding window from left until reaching the end
* Cases
  * 'A....A': 'A' = 'L' or 'R' ==> 'AAAAAA'
  * 'L....R' ==> no change
  * 'R....L' ==> 'RRRLLL'; 'R.....L' ==> 'RRR.LLL'
* Start & end process
  * If the first non-'.' symbol is 'L' ('....L') ==> 'LLLLL'
  * If the last non-'.' symbol is 'R' ('R....') ==> 'RRRRR'
* Complexity Analysis
  * Time: O(N), one scan
  * Space: O(N), one additional list



### Code

```python
class Solution:
    def pushDominoes(self, dominoes: str) -> str:
        # O(N) time, O(N) space
        if len(dominoes) <= 1: return dominoes
        pointer, ans = -1, list(dominoes)
        for i in range(len(dominoes)):
            if dominoes[i] != '.': 
                pointer = i
                if dominoes[i] == 'L': ans[:i] = 'L' * i
                break
        i = pointer
        while i < len(dominoes):
            if dominoes[i] == '.': i += 1
            elif dominoes[i] == dominoes[pointer]: 
                ans[pointer+1:i] = dominoes[i] * (i-pointer-1)
                i, pointer = pointer + 1, i
            else:
                if dominoes[i] == 'L':
                    # odd length, '.' in the center
                    if (i-pointer) % 2 == 0: 
                        ans[pointer+1:(i+pointer)//2] = dominoes[pointer] * ((i+pointer)//2 - pointer - 1)
                        ans[(i+pointer)//2+1:i] = dominoes[i] * (i - (i+pointer)//2 - 1)
                    # even length, no '.' in the center
                    else:
                        ans[pointer+1:(i+pointer+1)//2] = dominoes[pointer] * ((i+pointer+1)//2 - pointer - 1)
                        ans[(i+pointer+1)//2: i] = dominoes[i] * (i - (i+pointer+1)//2)
                i, pointer = pointer + 1, i
        if dominoes[pointer] == 'R': ans[pointer:] = 'R' * (len(dominoes) - pointer)
        return ''.join(ans)
```

