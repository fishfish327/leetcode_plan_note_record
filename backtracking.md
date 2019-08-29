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