# 451. Sort Characters By Frequency

2020/05/30 ZTH

### Problem Description

Given a string, sort it in decreasing order based on the frequency of characters.

**Example 1:**

```
Input:
"tree"

Output:
"eert"

Explanation:
'e' appears twice while 'r' and 't' both appear once.
So 'e' must appear before both 'r' and 't'. Therefore "eetr" is also a valid answer.
```



**Example 2:**

```
Input:
"cccaaa"

Output:
"cccaaa"

Explanation:
Both 'c' and 'a' appear three times, so "aaaccc" is also a valid answer.
Note that "cacaca" is incorrect, as the same characters must be together.
```



**Example 3:**

```
Input:
"Aabb"

Output:
"bbAa"

Explanation:
"bbaA" is also a valid answer, but "Aabb" is incorrect.
Note that 'A' and 'a' are treated as two different characters.
```



### Algorithm

* Use a dictionary to store the occurrence of each character in the string

* sort the dictionary by value in descending order

* for each key, value pair in the descending sorted dictionary, add the key character value times into the answer

* Complexity analysis

  * Time: O(nlogn) for worst case (sorting)
  * Space: O(n)

  