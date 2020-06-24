### 139. Word Break
LC link: https://leetcode.com/problems/word-break/

Author: XDDDD

Date: 06/23/2020

DP: Use an array to determine whether the substring from 0 to i can be splited by dict.

#### Code:
```java
class Solution {
    public boolean wordBreak(String s, List<String> wordDict) {
        int n = s.length();
        boolean[] dp = new boolean[n+1];
        Set<String> set = new HashSet<String>();
        for(String w:wordDict) set.add(w);
        dp[0] = true;
        for(int i = 1;i<=n;i++){
            for(int j = i-1;j>=0;j--){
                if(!dp[j]) continue;
                String sub = s.substring(j,i);
                if(set.contains(sub)){
                    dp[i] = true;
                    break;
                }
            }
        }
        return dp[n];
    }
}
```