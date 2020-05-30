### 647. Palindromic Substrings
Link: https://leetcode.com/problems/palindromic-substrings/
Author: Xiangde Zeng
Date: 05/29/2020  

#### Solution:
Use recursive, every time see an index as the middle point, tracking both sides to extend the palindrome. Need to be careful for even-length palindromes.

#### Code:
```Java
class Solution {
    int res;
    public int countSubstrings(String s) {
        res = 0;
        char[] str = s.toCharArray();
        for(int i = 0;i<s.length();i++){
            recursive(str,i);
        }
        return res;
    }
    
    public void recursive(char[] str, int idx){
        res++;
        if(idx == 0){
            return;
        }
        int l = idx-1;
        int r = idx+1;
        while(l >= 0 && r < str.length){
            if(str[l] != str[r]) break;
            res++;
            l--;
            r++;
        }
        
        if(str[idx] == str[idx-1]){
            res++;
            l = idx-2;
            r = idx+1;
            while(l >= 0 && r < str.length){
                if(str[l] != str[r]) break;
                res++;
                l--;
                r++;
            }
        }
        
    }
}
```