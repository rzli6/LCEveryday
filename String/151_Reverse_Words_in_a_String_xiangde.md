### 151. Reverse Words in a String
LC link: https://leetcode.com/problems/reverse-words-in-a-string/  
Author: Xiangde Zeng
Date: 06/07/2020

#### Solution : Reverse whole string then reverse the words
We can use two pointers to make an in-plcae reverse for this string
```Java
class Solution {
    public String reverseWords(String s) {
        //reverse entire string first, then reverse in words
        if(s.length() == 0) return s;
        char[] ch = s.toCharArray();
        removeSpaces(ch);
        int len = ch.length;

        reverse(ch,0,len-1);
        int start = 0;
        for(int i = 1;i<len;i++){
            if(ch[i] == ' '){
                reverse(ch,start,i-1);
                start = i+1;
            }
        }
        reverse(ch,start,len-1);
        String newStr = new String(ch);
        return newStr.trim();
    }
    
    void reverse(char[] ch, int l, int r){
        while(l < r){
            swap(ch,l++,r--);
        }
    }
    
    void removeSpaces(char[] ch){
        int len = 0;
        for(int i = 0;i<ch.length;i++){
            if(ch[i] != ' ') swap(ch,i,len++);
            else if(len != 0 && ch[len-1] != ' ') swap(ch,i,len++);
        }
    }
    
    void swap(char[] ch, int a ,int b){
        char temp = ch[a];
        ch[a] = ch[b];
        ch[b] = temp;
    }
}
```
