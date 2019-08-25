- 深拷贝问题， map 的典型应用
```java
public Node cloneGraph(Node node) {
        Map<Node, Node> map = new HashMap<>();
        if(node == null) return null;
        dfs(node, map);
        return map.get(node);
    }
    
    private void dfs(Node node, Map<Node, Node> map){
        if(node == null || map.containsKey(node))
            return;
        Node copyNode = new Node(node.val, new ArrayList<>());
        map.put(node, copyNode);
        for(Node neibor : node.neighbors){
            if(!map.containsKey(neibor))
                dfs(neibor ,map);
            Node copyNeibor = map.get(neibor);
            map.get(node).neighbors.add(copyNeibor);
        }
    }
```