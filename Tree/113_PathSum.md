# 113. Path Sum II

Author: LIU Zhuofei

## Problem
Given a binary tree and a sum, find all root-to-leaf paths where each path's sum equals the given sum.  
Example:  
Given the below binary tree and sum = 22,  
```
      5
     / \
    4   8
   /   / \
  11  13  4
 /  \    / \
7    2  5   1
```
Result:
```
[
   [5,4,11,2],
   [5,8,4,5]
]
```

## Ideas

**First idea:**  
BFS, get all the path and delete the list sum of which is not given sum.  
**How to do:**  
Use two queues or stacks to store TreeNode and path list respectively. So when I take the node, I also take the related path.  
Drawback: we need to delete some paths in the end. They will waste space.  

## Better answer from post

Source: [DFS with one LinkedList](https://leetcode.com/problems/path-sum-ii/discuss/36683/DFS-with-one-LinkedList-accepted-java-solution)  
Note: Pay attention to comments.  

```
public List<List<Integer>> pathSum(TreeNode root, int sum) {
    List<List<Integer>>ret = new ArrayList<List<Integer>>(); 
    List<Integer> cur = new ArrayList<Integer>(); 
    pathSum(root, sum, cur, ret);
    return ret;
}

public void pathSum(TreeNode root, int sum, List<Integer>cur, List<List<Integer>>ret){
    if (root == null){
        return; 
    }
    cur.add(root.val);
    if (root.left == null && root.right == null && root.val == sum){
        ret.add(new ArrayList(cur));
    }else{
        // divied problem into sub-problems
        pathSum(root.left, sum - root.val, cur, ret);
        pathSum(root.right, sum - root.val, cur, ret);
    }
    // backtracking
    cur.remove(cur.size()-1);
}
```

