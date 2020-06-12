# Elegant Code
## Some problems may be useless or easy, but I am surprised at code

## Terminate the Loop
```java
// 28. Implement strStr()
public int strStr(String haystack, String needle) {
  for (int i = 0; ; i++) {
    for (int j = 0; ; j++) {
      // Case 1: find the result
      if (j == needle.length()) return i;
      // Case 2: Finish the loop but no results
      if (i + j == haystack.length()) return -1;
      // Actual work
      if (needle.charAt(j) != haystack.charAt(i + j)) break;
    }
  }
}
```

## Double Pointer
Two pointer can start from index 0 to n-1.  
In some cases, maybe one or two pointers choose another direction from index n-1 to 0 can help improving the performance when we are in actual working environment.  

## Two hash map
[30. Substring with Concatenation of All Words](https://leetcode.wang/leetCode-30-Substring-with-Concatenation-of-All-Words.html)  
Hashmap can be one compareable item, HashMap can help us not to consider the **sequence** of string. 
