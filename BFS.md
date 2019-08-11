- 490. The Maze
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