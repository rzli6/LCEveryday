### [336. Palindrome Pairs](https://leetcode.com/problems/palindrome-pairs/)
Author: Xiangde Zeng
Date: 06/08/2020


#### Solution:
Consider the following three cases:
1. If the word is a palindrome, then find the index of empty string.
2. If the reverse of word exists, combine them to get a palindrome.
3. Split the word into prefix and suffix.
    3.1. If prefix is a palindrome, try to find the reverse string of suffix.
    3.2  If suffix is a palindrome, try to find the reverse string of prefix.

```Java
class Solution {
    public List<List<Integer>> palindromePairs(String[] words) {
        Map<String, Integer> map = new HashMap<String,Integer>();
        List<List<Integer>> res = new ArrayList<List<Integer>>();
        int n = words.length;

        for(int i = 0;i<n;i++){
            map.put(words[i],i);
        }
        
        for(int i = 0;i<n;i++){
            String w = words[i];
            if(w.equals("")) continue;
            if(isPalindrome(w) && map.containsKey("")){
                List<Integer> list = new ArrayList<Integer>();
                list.add(i);
                list.add(map.get(""));
                res.add(list);
                
                List<Integer> list2 = new ArrayList<Integer>();
                list2.add(map.get(""));
                list2.add(i);
                res.add(list2);
            }
            StringBuilder sb = new StringBuilder(w);
            sb.reverse();
            String r = sb.toString();
            if(map.containsKey(r) && map.get(r) != i){
                List<Integer> list = new ArrayList<Integer>();
                list.add(i);
                list.add(map.get(r));
                res.add(list);

            }
            int len = w.length();
            for(int j = 1;j<len;j++){
                String prefix = w.substring(0,j);
                String suffix = w.substring(j);
                if(isPalindrome(prefix)){
                    sb.setLength(0);
                    sb.append(suffix);
                    sb.reverse();
                    r = sb.toString();
                    if(map.containsKey(r)){
                        List<Integer> list = new ArrayList<Integer>();
                        list.add(map.get(r));
                        list.add(i);
                        res.add(list);
                    }
                }
                if(isPalindrome(suffix)){
                    sb.setLength(0);
                    sb.append(prefix);
                    sb.reverse();
                    r = sb.toString();
                    if(map.containsKey(r)){
                        List<Integer> list = new ArrayList<Integer>();
                        list.add(i);
                        list.add(map.get(r));
                        res.add(list);
                    }
                }
            }
        }
        return res;
    }
    
    boolean isPalindrome(String s){
        int n = s.length();
        int l = 0;
        int r = n - 1;
        while(l < r){
            if(s.charAt(l) != s.charAt(r)) return false;
            l++;
            r--;
        }
        return true;
    }
}
```
