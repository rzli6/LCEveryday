# 242. Valid Anagram

2020/06/16 Xiangde Zeng

### Problem Description

Given two strings s and t , write a function to determine if t is an anagram of s.

```
Input: s = "anagram", t = "nagaram"
Output: true
```

### Algorithm 
Count: Use 26-long array to records each character's count for string s. When counting t, we decrement each count numbers when iterating the string. If a character's count is nagative, then t would not be anagram. If all the counts are positive or 0, we can say t is the anagram of s.


```Java
class Solution {
    public boolean isAnagram(String s, String t) {
        if(s.length() != t.length()) return false;
        int[] counts = new int[26];
        for(int i = 0; i < s.length(); i++){
            char c = s.charAt(i);
            counts[c - 'a']++;
        }
        for(int i = 0;i < t.length();i++){
            char c = t.charAt(i);
            if(counts[c - 'a'] == 0) return false;
            counts[c - 'a']--;
        }
        return true;
    }
}
```

