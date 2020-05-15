# 非Leetcode: 用户最可能认识的人

Author: Xiangde Zeng

## Problem
给定一个含有N个用户的朋友列表，对于一个指定的用户，找出这个用户最可能认识的人。最可能认识的人的定义为这个人和当前用户不是朋友关系，但有最多的共同朋友。 若无，返回-1

 第一行两个数，第一个数为用户数目N，第二个数为需要判断的用户序号。
 之后每一行为每个用户的好友序号列表

Input:
```
5 0
1 2 3
0 4
0 4
0 4
1 2 3
```
Output:
```
 4
```

Explanation:
```
用户0 和 1 2 3都互相认识，用户4与用户1 2 3都互相认识
```

## Ideas

This question can be transformed to the graph problem: given a set of node and edges, for a particular node i, find a node j that has the most 2-length paths to node i.

```
public class FindFriend{
    public static void main(String[] args){
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        int id = sc.nextInt();
        sc.nextLine();

        List<List<Integer>> lists = new ArrayList<List<Integer>>();
        for(int i = 0;i<n;i++){
            lists.add(new ArrayList<Integer>());
            String line = sc.nextLine();
            String[] ids = line.split(" ");

            for(String s:ids){
                if(s.equals(""))continue;
                int j = Integer.valueOf(s);
                lists.get(i).add(j);

            }
        }
        int max = 0;
        int res = id;
        int[] counts = new int[n];
        for(int i : lists.get(id)){
            if(i == id) continue;
            counts[i] = -1;
            List<Integer> next_list = lists.get(i);
            for(int j:next_list){
                if(j == id || counts[j] == -1) continue;
                counts[j]++;
            }
        }

        for(int i = 0;i<n;i++){
            if(i == id || counts[i] == -1) continue;
            if(counts[i] > max){
                max = counts[i];
                res = i;
            }
        }
        if(res == id) System.out.println(-1);
        else  System.out.println(res);

    }



}
```

