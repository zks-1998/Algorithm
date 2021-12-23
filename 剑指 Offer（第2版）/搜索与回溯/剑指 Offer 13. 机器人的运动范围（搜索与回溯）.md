# 2021.12.15

## 剑指 Offer 13. 机器人的运动范围

地上有一个m行n列的方格，从坐标 [0,0] 到坐标 [m-1,n-1] 。一个机器人从坐标 [0, 0] 的格子开始移动，它每次可以向左、右、上、下移动一格（不能移动到方格外），也不能进入行坐标和列坐标的数位之和大于k的格子。例如，当k为18时，机器人能够进入方格 [35, 37] ，因为3+5+3+7=18。但它不能进入方格 [35, 38]，因为3+5+3+8=19。请问该机器人能够到达多少个格子？

示例 1：

```
输入：m = 2, n = 3, k = 1
输出：3
```

示例 2：

```
输入：m = 3, n = 1, k = 0
输出：1
```

提示：

```
1 <= n,m <= 100
0 <= k <= 20
```

### 解题方法

采用DFS+剪枝的方法

由于本题是统计合适的格子个数，所以每个格子仅需要访问一次就可以。从（0,0）开始访问，首先将访问数组标记为true，如果该位置符合要求，则+1，并朝其下、右两个方向遍历。不符合要求，则返回0，结束

### Java代码实现

```java
class Solution {
    public int movingCount(int m, int n, int k) {
        boolean[][] visited = new boolean[m][n]; // 设置空的访问数组
        return dfs(m,n,0,0,visited,k);
    }

    public int dfs(int m,int n,int i,int j,boolean [][]visited,int k){
        if(i < 0 || i >= m || j < 0 || j >= n || conut(i)+conut(j) > k || visited[i][j]){
            return 0; // 越界或者数字之和大于k或者已经被访问过，返回，因为若该点数字之和大于k,则其下节点和右节点必定均大于k，如果访问过，则其下节点和右节点也必定访问过了
        }else{
            visited[i][j] = true; // 标记访问 
            return 1 + dfs(m,n,i + 1,j,visited,k) + dfs(m,n,i,j + 1,visited,k); // 该节点复合，加1，递归遍历下节点、右节点
        }
    }
    public int conut(int num){
        if(num == 0) return 0;
        if(1 <= num && num <= 9) return num;
        if(10 <= num && num <= 99){
            int a = num % 10;
            int b = num / 10;
            return a + b;
        }else{
            return 1;
        }
    }
}
```

