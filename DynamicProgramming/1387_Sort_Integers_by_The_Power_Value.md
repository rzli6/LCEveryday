### 1387. Sort Integers by The Power Value
LC link: https://leetcode.com/problems/sort-integers-by-the-power-value/
Author: Xiangde Zeng
Date: 05/26/2020

#### Solution:  
Use Dynamic programming to store the result of each numbers. (Here, you can make the map as static for multiple test case to speed up.) Use head (PriorityQueue) to store the first k elements to get the k-th position.

#### Code:
```Java
class Solution {
    static Map<Integer,Integer> map;
    public int getKth(int lo, int hi, int k) {
        if(map == null){
            map = new HashMap<Integer,Integer>();
            map.put(1,0);
        }
        
        for(int i = lo;i <=hi;i++){
            if(map.containsKey(i)) continue;
            int val = i;
            findPower(val);
        }
        PriorityQueue<int[]> queue = new PriorityQueue<int[]>((a,b) -> (a[1] - b[1] == 0? a[0] - b[0] : a[1] - b[1]));
        for(int i = lo;i<=hi;i++){
            int[] set = new int[]{i,map.get(i)};
            queue.offer(set);
        }
        for(int i = 0;i<k-1;i++) queue.poll();
        return queue.poll()[0];
        
    }
    
    int findPower(int val){
        if(map.containsKey(val)) return map.get(val);
        if(val % 2 == 0){
            int res = 1 + findPower(val/2);
            map.put(val,res);
            return res;
        }
        else{
            int res = 1 + findPower(3 * val + 1);
            map.put(val,res);
            return res;
        }
        
    }
}
```