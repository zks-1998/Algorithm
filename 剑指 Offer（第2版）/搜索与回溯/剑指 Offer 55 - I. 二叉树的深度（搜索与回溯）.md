# 2021.12.18

## 剑指 Offer 55 - I. 二叉树的深度

输入一棵二叉树的根节点，求该树的深度。从根节点到叶节点依次经过的节点（含根、叶节点）形成树的一条路径，最长路径的长度为树的深度

例如：

给定二叉树 [3,9,20,null,null,15,7]



​    3

   / \
  9  20
      /  \
    15   7
返回它的最大深度 3 

### 解题方法

先序遍历+回溯

### Java代码实现

```java
class Solution {
    int count,max;
    public int maxDepth(TreeNode root) {
        dfs(root);
        return max;
    }
    void dfs(TreeNode node){
        if(node == null) return;
        count += 1;
        max = Math.max(count,max);
        dfs(node.left);
        dfs(node.right);  
        count -=1 ;
    }

}
```

