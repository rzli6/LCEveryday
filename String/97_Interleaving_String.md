# 97. Interleaving String

2020/06/16 Xiangde Zeng

### Problem Description

Given s1, s2, s3, find whether s3 is formed by the interleaving of s1 and s2.

```
Input: s1 = "aabcc", s2 = "dbbca", s3 = "aadbbcbcac"
Output: true
```

### Algorithm 1
DFS: Using recuesion to track the whole string to get the result


```Java
class Solution {
    public boolean isInterleave(String s1, String s2, String s3) {
        char[] s1_ch = s1.toCharArray();
        char[] s2_ch = s2.toCharArray();
        char[] s3_ch = s3.toCharArray();
        return track(s1_ch,s2_ch,s3_ch,0,0,0);
    }
    
    boolean track(char[] s1, char[] s2, char[] s3, int i, int j, int k){
        if(i == s1.length && j == s2.length && k == s3.length) return true;
        if(k == s3.length) return false;
        if(i == s1.length && j == s2.length) return false;
        if(i == s1.length && j < s2.length){
            if(s2[j] != s3[k]) return false;
            return track(s1,s2,s3,i,j+1,k+1);
        }
        if(j == s2.length && i < s1.length){
            if(s1[i] != s3[k]) return false;
            return track(s1,s2,s3,i+1,j,k+1);
        }
        if(s1[i] == s3[k]){
            if(track(s1,s2,s3,i+1,j,k+1)) return true;
        }
        if(s2[j] == s3[k]){
            if(track(s1,s2,s3,i,j+1,k+1)) return true;
        }
        return false;
    }
}
```

### Algorithm 2
DP: We can transform the recursion above into 2D dynamic programing: dp[i][j] stands for whetehr we can get a i + j length of interleved string with i-len string 1 and j-len string j. Initially, dp[0][0] = true as two empty strings can combined an empty string. In the follwing iterations, we only need to check whether the previous iteration is true or not while the current index can match the interleved string. 

```Java
class Solution {
    public boolean isInterleave(String s1, String s2, String s3) {
        char[] s1_ch = s1.toCharArray();
        char[] s2_ch = s2.toCharArray();
        char[] s3_ch = s3.toCharArray();
        int n = s1_ch.length;
        int m = s2_ch.length;
        int l = s3_ch.length;
        if(n + m != l) return false;
        boolean[][] dp = new boolean[n+1][m+1];
        dp[0][0] = true;
        for(int i = 0;i <= n;i++){
            for(int j = 0;j<=m;j++){
                if(i > 0) dp[i][j] = dp[i-1][j] && s3_ch[i + j - 1] == s1_ch[i-1];
                if(j > 0) dp[i][j] = dp[i][j] || (dp[i][j-1] && s3_ch[i+j-1] == s2_ch[j-1]);
            }
        }
        return dp[n][m];
    }
    

}
```
