# 56. Merge Intervals

2020/06/21 XDDD

### Problem Description

Given a collection of intervals, merge all overlapping intervals.

### Algorithm

1. Sort the array first, and merge the overlapping part

   ```java
   class Solution {
       public int[][] merge(int[][] intervals) {
           Arrays.sort(intervals,(a,b) -> (a[0] == b[0]?a[1]-b[1]:a[0]-b[0]));
           List<int[]> list = new LinkedList<int[]>();
           int l = 0;
           int r = -1;
           for(int[] i:intervals){
               if(r < l){
                   l = i[0];
                   r = i[1];
                   continue;
               }
               if(r < i[0]){
                   int[] gap = new int[2];
                   gap[0] = l;
                   gap[1] = r;
                   list.add(gap);
                   l = i[0];
                   r = i[1];
               }
               else{
                   r = Math.max(r,i[1]);
               }
           }
           if(l <= r){
               int[] gap = new int[2];
               gap[0] = l;
               gap[1] = r;
               list.add(gap);
           }
           int n = list.size();
           int[][] res = new int[n][2];
           for(int i = 0;i<n;i++){
               int[] gap = list.get(i);
               res[i][0] = gap[0];
               res[i][1] = gap[1];
           }
           return res;
       }
   }
   ```

   

2. Use two arrays, starts and ends, to sort the intervals. Use two pointers to track the overlapping gap.

   ```java
   class Solution {
       public int[][] merge(int[][] intervals) {
           int len = intervals.length;
           int[] start = new int[len];
           int[] end = new int[len];
           for(int i = 0;i<len;i++){
               start[i] = intervals[i][0];
               end[i] = intervals[i][1];
           }
           Arrays.sort(start);
           Arrays.sort(end);
           int l = 0;
           int r = 0;
           List<int[]> list = new LinkedList<int[]>();
           for(r = 0;r<len;r++){
               if(r == len - 1 || start[r+1] > end[r]){
                   int[] gap = new int[2];
                   gap[0] = start[l];
                   gap[1] = end[r];
                   list.add(gap);
                   l = r + 1;
               }
           }
           
           int n = list.size();
           int[][] res = new int[n][2];
           for(int i = 0;i<n;i++){
               int[] gap = list.get(i);
               res[i][0] = gap[0];
               res[i][1] = gap[1];
           }
           return res;
       }
   }
   ```

   