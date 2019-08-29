##### 99. Recover Binary Search Tree
- 二分查找树的inorder traverse 得到有序序列
- inorder traverse的解法如下：
```java
class Solution {
    TreeNode firstElement = null;
    TreeNode secondElement = null;
    // The reason for this initialization is to avoid null pointer exception in the first comparison when prevElement has not been initialized
    TreeNode prevElement = new TreeNode(Integer.MIN_VALUE);
    
    public void recoverTree(TreeNode root) {
        
        // In order traversal to find the two elements
        traverse(root);
        
        // Swap the values of the two nodes
        int temp = firstElement.val;
        firstElement.val = secondElement.val;
        secondElement.val = temp;
    }
    
    private void traverse(TreeNode root) {
        
        if (root == null)
            return;
            
        traverse(root.left);
        
        // Start of "do some business", 
        // If first element has not been found, assign it to prevElement (refer to 6 in the example above)
        if (firstElement == null && prevElement.val >= root.val) {
            firstElement = prevElement;
        }
    
        // If first element is found, assign the second element to the root (refer to 2 in the example above)
        if (firstElement != null && prevElement.val >= root.val) {
            secondElement = root;
        }        
        prevElement = root;

        // End of "do some business"

        traverse(root.right);
}
}
```
- 常数空间的inorder traverse : morris traversel
```c
void inorderMorrisTraversal(TreeNode *root) {
    TreeNode *cur = root, *prev = NULL;
    while (cur != NULL)
    {
        if (cur->left == NULL)          // 1.
        {
            printf("%d ", cur->val);
            cur = cur->right;
        }
        else
        {
            // find predecessor
            prev = cur->left;
            while (prev->right != NULL && prev->right != cur)
                prev = prev->right;

            if (prev->right == NULL)   // 2.a)
            {
                prev->right = cur;
                cur = cur->left;
            }
            else                       // 2.b)
            {
                prev->right = NULL;
                printf("%d ", cur->val);
                cur = cur->right;
            }
        }
    }
}
```

##### lc 117. Populating Next Right Pointers in Each Node II
- 思路， 层序遍历， 记录下一层的head 和 tail, 在遍历本层的时候， 下面一层已经被connect

##### lc house robber 3
- 思路： 分rob和 unrob的情况分别计算， tree的递归
```java
//注意这里unrob的时候， 下面的节点是随便取的
res[1] = leftV[0] + rightV[0] + root.val;
res[0] = Math.max(leftV[0], leftV[1]) + Math.max(rightV[0], rightV[1]);
```

##### lc largest increase tree
- 最初的思路， 通过pq, 从最小的开始计算
- 优化： 其实使用dfs可以确保从最大值开始生成step, 同时减少遍历次数
```java
public int longestIncreasingPath(int[][] matrix) {
        if(matrix.length == 0 || matrix[0].length == 0)
            return 0;
        int m = matrix.length, n = matrix[0].length;
        int res = 1;
        int[][] dp = new int[m][n];
        for(int i = 0; i < m; i++){
            for(int j = 0; j < n; j++){
                res = Math.max(res, dfs(matrix, dp, i, j));
            }
        }
        return res;
    }
    private int dfs(int[][] matrix, int[][] dp, int i, int j){
        int m = matrix.length, n = matrix[0].length;
        if(dp[i][j] != 0)
            return dp[i][j];
        int[][] dirs = {{0,1},{0,-1},{1,0},{-1,0}};
        for(int[] dir : dirs){
            int x = dir[0] + i;
            int y = dir[1] + j;
            if(x >=0 && x < m && y >=0 && y < n && matrix[i][j] < matrix[x][y]){
                dp[i][j] = Math.max(dp[i][j], dfs(matrix, dp, x, y));
            }
            
        }
        return ++dp[i][j]; 
    }
```
##### 133 clone graph
- 深拷贝问题， map 的典型应用
##### 472 Concatenated Words
- 注意的问题： substr不在words里面的时候不进行dfs
- 题解参考： 结合Tries
##### 652 duplicated tree
- 这道题在遍历的思路上可以使用DFS, 记录之前的遇到过的子状态， 问题的突破点在于如何记录， 记录什么
- 解法参考： 将数序列化

##### 272 k close value
- 树的遍历
- 参考解法1： 使用pq
- 参考解法2： linkedList, 先把list填满， 然后poll出不符合条件的