# 648. Replace Words

2020/06/20 ZTH

### Problem Description

In English, we have a concept called `root`, which can be followed by some other words to form another longer word - let's call this word `successor`. For example, the root `an`, followed by `other`, which can form another word `another`.

Now, given a dictionary consisting of many roots and a sentence. You need to replace all the `successor` in the sentence with the `root` forming it. If a `successor` has many `roots` can form it, replace it with the root with the shortest length.

You need to output the sentence after the replacement.

**Example 1:**

```
Input: dict = ["cat","bat","rat"], sentence = "the cattle was rattled by the battery"
Output: "the cat was rat by the bat"
```

**Constraints:**

- The input will only have lower-case letters.
- `1 <= dict.length <= 1000`
- `1 <= dict[i].length <= 100`
- 1 <= sentence words number <= 1000
- 1 <= sentence words length <= 1000



### Algorithm

Base idea: We hash the prefix of each word for each possible prefix and check whether the prefix exists in the given roots

* Use a set() to store all the given roots (faster when check whether prefix exists in roots)

* For each word in the given sentence, we start from the first character as prefix, each time adding one character until the whole word as the prefix

  * ```
    e.g. given word: cattle
    	   prefix:     c -> ca -> cat -> catt -> cattl -> cattle
    ```

  * This makes sure we check prefix with smaller length first, which satisfies the requirement of shortest length root for a tie.

  * Once we find the prefix in the given root set, replace this word with this prefix and continue for next word.

* Complexity Analysis

  * Time: O(sum of length-i^2), where length-i is the length of the i-th word. For each word, we start from the only one character as the prefix to the whole word, the complexity for single word is O(length-i^2)
  * Space: O(N + R), root length + sentence length



### Code

```python
class Solution:
    def replaceWords(self, dict: List[str], sentence: str) -> str:
        root, l = set(dict), sentence.split()
        for index in range(len(l)):
            for i in range(len(l[index])):
                if l[index][:i] in root:
                    l[index] = l[index][:i]
                    break
        return ' '.join(l)
```

