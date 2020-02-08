- lc 490 The Maze
这道题的题意解析： 撞到墙之后， 小球的方向才可以改变
解决思路： 
- 还是可以用BFS的思路， 要变动的地方在于， 需要一直走，走到撞墙为止，
- 其余步数选择， 状态记录，和通常的BFS并无区别
解法记录：
```java
int[][] direction = new int[][] {{-1,0},{1,0},{0.-1},{0,1}};
int[] curr = list.poll();
int x = curr[0], y = curr[1];
for(int[] dir : direction){
    int xx = x, yy = y;
    while(xx >=0 && xx < m && yy >= 0 && yy <= n && maze[xx][yy] == 0){
        xx += dir[0];
        yy += dir[1];
    }
    xx -= dir[0];
    yy -= dir[1];
    if(visited[xx][yy]) continue;
    // 后续略
}
```
- lc 815 bus routes
这道题我的解决思路还是比较直接， 需要注意的一个问题是判断路径的重合
速度如何进一步优化， 其他题解的学习。
和高票的本质不同， 使用bus stop 来进行BFS还是用bus route进行。
优化点： 1 记录stop -> route 的关系， 避免每次进行遍历
        2 由于站点数远多于路线数， 因此记录visited stop 也可以大大的优化运行时间
附代码如下
```java
private void addToQueue(List<Integer> list, boolean[] visited, Queue<Integer> queue){
        for(int i : list){
            if(visited[i]){
                continue;
            }
            queue.add(i);
            visited[i] = true;

        }
        
    }
```
- lc 847 Shortest path visited all path
 首次回答 可否做出？ 不能、无法套用BFS
 dp 和位运算的结合， 待进一步学习

#####  lc 773 sliding puzzle 
- 无法首次回答
- 这道题的关键是如何表示状态， 高票中把棋盘压缩成字符串是个高效的做法
#####  由上一道的棋盘问题， 回顾 N-queens 问题
- 使用borad 记录棋盘状态， backtracking 进行状态回退
```java
private void dfs(char[][] board, int colIndex)
	{
		if(colIndex == board.length){
            res.add(construct(board));
            return;
        }
        for(int i = 0; i < board.length; i++){
            if(validate(board, i, colIndex)){
                board[i][colIndex] = 'Q';
                dfs(board, colIndex + 1);
                board[i][colIndex] = '.';
            }
            
        }
	}
```
##### lc 261 graph valid tree
- 我的解法： 无向图是否为树的判定： 无环 + 连通， BFS遍历节点
- 高票 union find 解法
```java
public boolean validTree(int n, int[] edges){
// init 用一维数组来表示点点之间的关系
int[] nums = new int[n];
Arrays.fill(nums, -1);
// perform union find
for(int[] edge : edges){
    int a = find(nums, edge[0]);
    int b = find(nums, edge[1]);
    if(a == b) return false;
    nums[a] = b;
}
// 通过边的数量加以验证
return edges.length == n - 1;
}
private int find(int[] nums, int i){
    if(nums[i] == -1) return i;
    return find(nums, nums[i]);
}
``` 
- DFS 解法， 注意环的判定方法， 思考： tree 的递归和DFS的联系
```java
boolean hasCycle(List<List<Integer>> adjList, int u, boolean[] visited, int parent]){
    visited[u] = true;
    for(int i =0; i < adjList.get(u).size(); i++){
        int v = adjList.get(u).get(i);
        if(
            (visited[v] && parent != v) ||
            (!visited[v] && hasCycle(adjList, v, visited, u))
        )
        return true;
    }
    return false;
}
```
##### 286 walls and gates , BFS 模板题型
##### 42 trapping rain watter
- 将计算转换为计算单个区间， 寻找left max 和 right max 
