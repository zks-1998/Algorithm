#                                 2021年12月14日

## 剑指 Offer 12. 矩阵中的路径

给定一个 m x n 二维字符网格 board 和一个字符串单词 word 。如果 word 存在于网格中，返回 true ；否则，返回 false 。单词必须按照字母顺序，通过相邻的单元格内的字母构成，其中“相邻”单元格是那些水平相邻或垂直相邻的单元格。同一个单元格内的字母不允许被重复使用。

例如，在下面的 3×4 的矩阵中包含单词 "ABCCED"（单词中的字母已标出）。

![image-20211214213656722](C:\Users\zhangkunsong\AppData\Roaming\Typora\typora-user-images\image-20211214213656722.png)

### 解题方法

本题采用DFS+剪枝+回溯法

- **深度优先搜索：**可以理解为暴力法遍历矩阵中所有字符串可能性。DFS 通过递归，先朝一个方向搜到底，再回溯至上个节点，沿另一个方向搜索，以此类推
- **剪枝：**在搜索中，遇到这条路不可能和目标字符串匹配成功的情况（*例如：此矩阵元素和目标字符不同、此元素已被访问）*，则应立即返回，称之为可行性剪枝

### 相关参数

**递归参数：**

 当前元素在矩阵 `board` 中的行列索引 `i` 和 `j` ，当前目标字符在 `word` 中的索引 `k`

**终止条件：**

返回 false ： (1) 行或列索引越界 或 (2) 当前矩阵元素与目标字符不同 或 (3) 当前矩阵元素已访问过 （ (3) 可合并至 (2) ） 
返回 true ： `k = len(word) - 1` ，即字符串 word 已全部匹配

**递推工作：**
1.标记当前矩阵元素： 将` board[i][j]`修改为空字符'\0' ，代表此元素已访问过，防止之后搜索时重复访问 

2.搜索下一单元格： 朝当前元素的 上、下、左、右 四个方向开启下层递归，使用 或 连接 （代表只需找到一条可行路径就直接返回，不再做后续 DFS ），并记录结果至 res 

3.还原当前矩阵元素： 将` board[i][j]` 元素还原至初始值，即 word[k] ，假如上题要求我们找ABCCF，我们以B为中心进行搜索时，会把F变成空，如果不还原，当我们到了（1,2）C后，将找不到F，所以不管找不找得到，都要还原

### Java代码实现

```java
class Solution {
    public boolean exist(char[][] board, String word) {
        char []words = word.toCharArray();
        for(int i = 0;i < board.length;i++){
            for(int j = 0;j < board[0].length;j++){
                if(dfs(board,words,i,j,0)) return true;
            }
        }
        return false;
    }

    public static boolean dfs(char[][]board,char[] word,int i,int j,int k){
        if(i >= board.length || i < 0 || j >= board[0].length || j < 0 || board[i][j] != word[k]) 
        return false;
        if(k == word.length - 1) return true;
        board[i][j] = '\0';
        boolean res = dfs(board,word,i + 1,j,k+1) || dfs(board,word,i-1,j,k + 1) ||
                      dfs(board,word,i,j+1,k+1) ||dfs(board,word,i,j-1,k+1);
        board[i][j] = word[k];
        return res;
    }
}
```


