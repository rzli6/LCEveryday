### 1192. Critical Connections in a Network
LC link: https://leetcode.com/problems/critical-connections-in-a-network/
Author: XDDDD
Date: 06/17/2020

#### Solution:
Tarjan Algorithm: https://blog.csdn.net/D5__J9/article/details/100922207

#### Code:
```Java
class Solution {
    List<List<Integer>> res;
    List<List<Integer>> graph;
    int t = 1;
    public List<List<Integer>> criticalConnections(int n, List<List<Integer>> connections) {
        res = new ArrayList<List<Integer>>();
        if(n == 0) return res;
        graph = new ArrayList<List<Integer>>();
        for(int i = 0; i < n;i++){
            graph.add(new ArrayList<Integer>());
        }
        for(List<Integer> ls:connections){
            int n1 = ls.get(0);
            int n2 = ls.get(1);
            graph.get(n1).add(n2);
            graph.get(n2).add(n1);
        }
        int[] dfn = new int[n];
        int[] low = new int[n];
        int[] parent = new int[n];
        tarjan(0,dfn,low,parent);
        return res;
    }
    
    public void tarjan(int cur, int[] dfn, int[] low, int[] parent){
        if(dfn[cur] != 0) return;
        dfn[cur] = low[cur] = t++;
        for(int next : graph.get(cur)){
            if(parent[cur] == next) continue;
            parent[next] = cur;
            if(dfn[next] == 0){
                tarjan(next,dfn,low,parent);
                low[cur] = Math.min(low[cur],low[next]);
                if(low[next] > dfn[cur]){
                    List<Integer> ls = new ArrayList<Integer>();
                    ls.add(cur);
                    ls.add(next);
                    res.add(ls);
                }
            }
            else if(dfn[next] < low[cur]) low[cur] = dfn[next];
        }
    }
}
```

