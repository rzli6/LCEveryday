### [387. First Unique Character in a String](https://leetcode.com/problems/first-unique-character-in-a-string/)
Author: Xiangde Zeng
Date: 06/08/2020


#### Solution:
Allocate a 26-length array to record the first position of each character. If a character appears twice or more, set the position to -2 to indicate it is duplicated.

```Java
class Solution {
    public int firstUniqChar(String s) {
        int[] pos = new int[26];
        Arrays.fill(pos,-1);
        for(int i = 0; i<s.length();i++){
            char c = s.charAt(i);
            if(pos[c - 'a'] >= 0) pos[c - 'a'] = -2;
            else if(pos[c - 'a'] == -1) pos[c - 'a'] = i;
        }
        int idx = s.length();
        for(int i : pos){
            if(i < 0) continue;
            idx = Math.min(i,idx);
        }
        if(idx == s.length()) return -1;
        return idx;
    }
}
```
