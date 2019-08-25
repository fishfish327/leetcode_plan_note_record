##### 407
```java
public int trapRainWater(int[][] heightMap) {
        if(heightMap.length <= 2 || heightMap[0].length <= 2)
            return 0;
        int m = heightMap.length, n = heightMap[0].length;
        boolean[][] visited = new boolean[m][n];
        PriorityQueue<int[]> pq = new PriorityQueue<>(1, (a, b) -> a[2] - b[2]);
        for(int i = 0; i < m; i++){
            pq.add(new int[]{i, 0, heightMap[i][0]});
            pq.add(new int[]{i, n-1, heightMap[i][n-1]});
            visited[i][0] = true;
            visited[i][n-1] = true;
        }
        for(int j = 0; j < n; j++){
            pq.add(new int[]{0, j, heightMap[0][j]});
            pq.add(new int[]{m-1, j, heightMap[m-1][j]});
            visited[0][j] = true;
            visited[m-1][j] = true;
        }
        int res = 0;
        while(!pq.isEmpty()){
            int[] curr = pq.poll();
            int[][] move = {{0,1},{0,-1},{1,0},{-1,0}};
            for(int[] step : move){
                int x = step[0] + curr[0];
                int y = step[1] + curr[1];
                
                if(0 <= x && x < m && 0 <= y && y < n
                  && !visited[x][y]
                  ){
                    visited[x][y] = true;
                    res += Math.max(0, curr[2] - heightMap[x][y]);
                    pq.offer(new int[]{x, y, Math.max(heightMap[x][y], curr[2])});
                }
            }
        }
        return res; 
```
- 这道题的思路: 寻找边界，通过BFS不断更新边界， 在边界处选取最小值
- 需要注意的问题： pq里面存储的border 其实是“加了水之后的border”, 不在是heightMap里面的值了

##### trapping rain water 1d
```java
public int trap(int[] A){
    int a=0;
    int b=A.length-1;
    int max=0;
    int leftmax=0;
    int rightmax=0;
    while(a<=b){
        leftmax=Math.max(leftmax,A[a]);
        rightmax=Math.max(rightmax,A[b]);
        if(leftmax<rightmax){
            max+=(leftmax-A[a]);       // leftmax is smaller than rightmax, so the (leftmax-A[a]) water can be stored
            a++;
        }
        else{
            max+=(rightmax-A[b]);
            b--;
        }
    }
    return max;
}
```