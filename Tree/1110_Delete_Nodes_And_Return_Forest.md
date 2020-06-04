### 1110. Delete Nodes And Return Forest
LC link: https://leetcode.com/problems/delete-nodes-and-return-forest/
Author: Xiangde Zeng
Date: 06/03/2020

#### Solution:
Idea: DFS. When a node is mark as a root, add it to the list. If a node needs to be deleted, mark its left and right child as root and unlink the parentship with its child node and its parent node.

#### Code:
```Java
class Solution {
    List<TreeNode> res;
    Set<Integer> set;
    public List<TreeNode> delNodes(TreeNode root, int[] to_delete) {
        res = new ArrayList<TreeNode>();
        if(root == null) return res;
        set = new HashSet<Integer>();
        for(int i : to_delete) set.add(i);
        dfs(root,null,true);
        return res;
    }
    
    void dfs(TreeNode node, TreeNode parent, boolean isRoot){
        if(node == null) return;
        boolean isDel = set.contains(node.val);
        dfs(node.left, node ,isDel);
        dfs(node.right, node, isDel);
        if(isRoot && !isDel){
            res.add(node);
        }
        if(!isRoot && isDel){
            if(parent != null){
                if(parent.left == node) parent.left = null;
                else if(parent.right == node) parent.right = null;
            }
            node.left = null;
            node.right = null;
        }
    }
    
    
}
```                
