##### tries 的实现参考
```java
    private static final int R = 26;
    private TrieNode root;
    
    private static class TrieNode {
        private final TrieNode[] children;
        private boolean isWord;
        
        private TrieNode() {
            children = new TrieNode[R];
            isWord = false;
        }
    }
    
    private void insertWord(String word) {
        TrieNode curr = root;
        int len = word.length(), idx;
        char c;
        
        for (int i = 0; i < len; ++i) {
            c = word.charAt(i);
            idx = c - 'a';
            if (curr.children[idx] == null) curr.children[idx] = new TrieNode();
            curr = curr.children[idx];
        }
        curr.isWord = true;
    }
```