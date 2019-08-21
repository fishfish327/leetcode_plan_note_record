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
