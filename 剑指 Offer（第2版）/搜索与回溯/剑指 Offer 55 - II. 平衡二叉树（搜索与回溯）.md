# 2021.12.19

## 剑指 Offer 55 - II. 平衡二叉树

输入一棵二叉树的根节点，判断该树是不是平衡二叉树。如果某二叉树中任意节点的左右子树的深度相差不超过1，那么它就是一棵平衡二叉树

给定二叉树 [3,9,20,null,null,15,7]

​    3

   / \
  9  20
    /  \
   15   7
返回 true 



### 解题思路

先写一个求树高的函数，然后递归判断树的任何一个节点是否符合平衡二叉树

### Java代码实现

```java
class Solution {
    public boolean isBalanced(TreeNode root) {
       if(root == null){
           return true;
       }else{
           return Math.abs(depth(root.right) - depth(root.left)) <= 1 && isBalanced(root.left) && isBalanced(root.right);
       }
    }
    int depth(TreeNode node){
         if (node == null) {
            return 0;
        } else {
            return Math.max(depth(node.left),depth(node.right)) + 1;
        }
}
}
```

