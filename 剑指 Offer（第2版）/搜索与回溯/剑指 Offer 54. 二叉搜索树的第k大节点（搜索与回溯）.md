# 2021.12.18

## 剑指 Offer 54. 二叉搜索树的第k大节点

给定一棵二叉搜索树，请找出其中第k大的节点

```
输入: root = [3,1,4,null,2], k = 1
   3
  / \
 1   4
  \
   2
输出: 4


```

```
输入: root = [5,3,6,2,4,null,null,1], k = 3
       5
      / \
     3   6
    / \
   2   4
  /
 1
输出: 4
```

### 解题方法

中序遍历即可，设置一个计数器，若count == k，记录当前节点，返回值即可

### Java代码实现

```java
class Solution {
    int count;
    TreeNode res;
    public int kthLargest(TreeNode root, int k) {
        inOrder(root,k);
        return res.val;
    }

    void inOrder(TreeNode node,int n){
        if(node == null) return;
        inOrder(node.right,n);
        count += 1;
        if(count == n) res = node;
        inOrder(node.left,n);
    }
}
```



