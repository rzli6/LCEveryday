# 49. Group Anagrams

2020/05/24 ZTH

### Problem Description

Given an array of strings, group anagrams together.

**Example:**

```
Input: ["eat", "tea", "tan", "ate", "nat", "bat"],
Output:
[
  ["ate","eat","tea"],
  ["nat","tan"],
  ["bat"]
]
```

**Note:**

- All inputs will be in lowercase.
- The order of your output does not matter.



### Algorithm

* use a dictionary to store each anagram

  ```
  e.g. 'a': 1, 'e': 1, 't': 1 ==> eat, tea, ate
  ```

* the key point is how to store the anagram

  * use dictionary as the key: dictionary cannot be directly used as a key for another dictionary

    ```
    e.g. {{'a': 1, 'e': 1, 't': 1}: ['eat', 'tea', 'ate']} is not okay for direct use
    ==>
    utilize Python's frozenset function
    ```

  * use string as the key:

    * for each element, we maintain a length 26 string showing each character's number in the item.

      ```
      e.g. eat ==> 100010000...001..00
      			       abcdefghi...rst..yz
      ```

* Complexity analysis

  * O(NK) time, N = # items, K = maximum item length

  * O(NK) space

    

### Code

```python
class Solution:
    def groupAnagrams(self, strs: List[str]) -> List[List[str]]:            
        # way1: python forzenset ==> O(NK) time, O(NK) space
        dic, ans = {}, []
        for e in strs:
            current = collections.Counter(e)
            current = frozenset(current.items())
            if current not in dic: dic[current] = [e]
            else: dic[current].append(e)
        for key, value in dic.items():
            ans.append(value)
        return ans
```



```python
class Solution:
    def groupAnagrams(self, strs: List[str]) -> List[List[str]]:
        # way1: string for key ==> O(NK) time, O(NK) space
        dic, ans = {}, []
        for e in strs:
            template = [0 for i in range(26)]
            for i in e:
                template[ord(i)-ord('a')] += 1
            template = ''.join(str(x) for x in template)
            if template not in dic: dic[template] = [e]
            else: dic[template].append(e)
        for key, value in dic.items():
            ans.append(value)
        return ans
```

