# 2021.12.17

## 剑指 Offer 34. 二叉树中和为某一值的路径

给你二叉树的根节点 root 和一个整数目标和 targetSum ，找出所有 从根节点到叶子节点 路径总和等于给定目标和的路径

叶子节点 是指没有子节点的节点

![image-20211221150135670](C:\Users\zhangkunsong\AppData\Roaming\Typora\typora-user-images\image-20211221150135670.png)



```
输入：root = [5,4,8,11,null,13,4,7,2,null,null,5,1], targetSum = 22
输出：[[5,4,11,2],[5,8,4,5]]
```

### 解题方法

采用先序遍历+回溯的方法，先计算5,4,11,7，不合适回溯，计算5,4,11,2，类推。具体怎么回溯？可以用LinkedList.removeLast()方法

### Java代码实现

```java
lass Solution {
    ArrayList<List<Integer>> res = new ArrayList<>(); // 结果集合
    LinkedList<Integer> path = new LinkedList<>(); // 回溯专用集合
    public List<List<Integer>> pathSum(TreeNode root, int target) {
        recur(root,target);
        return res;
    }

    void recur(TreeNode node,int target){
        if(node == null) return;
        path.add(node.val); // 路径值加入回溯集合
        target = target - node.val; // 更新目标值
        if(target == 0 && node.left == null && node.right == null){ 
            res.add(new ArrayList(path)); // 符合条件复制列表加入到结果集合
        }
        recur(node.left,target); // 先序遍历
        recur(node.right,target);
        path.removeLast(); // 回溯
    }
}
```

