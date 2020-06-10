# 1177. Can Make Palindrome from Substring

2020/06/10 ZLY

### Problem Description

Given a string `s`, we make queries on substrings of `s`.

For each query `queries[i] = [left, right, k]`, we may **rearrange** the substring `s[left], ..., s[right]`, and then choose **up to** `k` of them to replace with any lowercase English letter. 

If the substring is possible to be a palindrome string after the operations above, the result of the query is `true`. Otherwise, the result is `false`.

Return an array `answer[]`, where `answer[i]` is the result of the `i`-th query `queries[i]`.

Note that: Each letter is counted **individually** for replacement so if for example `s[left..right] = "aaa"`, and `k = 2`, we can only replace two of the letters. (Also, note that the initial string `s` is never modified by any query.)



### Algorithm

The rough idea is that we can calculate how many numbers that occur odd times in the query substring (denoted as `n`). And if `k>n//2`, then it means the substring can form a palindrome.

To save time, we use prefix records to continuously update the number of odd occurrences.



### Code

```python
def canMakePaliQueries(self, s: str, queries: List[List[int]]) -> List[bool]:
    alphabet = set(s) #只处理在s中出现过的字母
    dic = dict()
    for char in alphabet:
        dic[char] = [0 for _ in range(len(s))]

    for i, ch in enumerate(s): #计算出现次数的前缀和
        for char in alphabet:
            if ch == char:
                if i > 0:
                    dic[char][i] = dic[char][i - 1] + 1
                else:
                    dic[char][i] = 1
            else:
                if i > 0:
                    dic[char][i] = dic[char][i - 1] 

    result = []
    for left, right, k in queries:
        odd_cnt = 0
        for char in alphabet:
            if left > 0:
                if (dic[char][right] - dic[char][left - 1]) % 2 == 1:# 直接相减得到字母出现次数
                    odd_cnt += 1
            else:
                if dic[char][right] % 2 == 1:
                    odd_cnt += 1
        if odd_cnt // 2 <= k:
            result.append(True)
        else:
            result.append(False)                
    return result
```