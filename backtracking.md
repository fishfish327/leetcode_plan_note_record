##### 数独解法
```java
private boolean backtracking(char[][] board){
        for(int i = 0; i < 9; i++){
            for(int j = 0; j < 9; j++){
                if(board[i][j] == '.'){
                    List<Character> list = getChars(board,i, j);
                    for(char c : list){
                        board[i][j] = c;
                        if(backtracking(board)){
                            return true;
                        } else {
                            board[i][j] = '.';
                        }
                    }
                    return false;
                }
            }
        }
        return true;
    }
```

##### word pattern
- 基本思路： 尝试所以可能长度的匹配方案，失败则回退
- 注意： 区分失败， 和跳过， 遇到重复的str时应该跳过而不是直接return false。 
- api: String.startsWith(index, str)