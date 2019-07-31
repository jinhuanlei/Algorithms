## Deep Copy Undirected Graph
Make a deep copy of an undirected graph, 
there could be cycles in the original graph.
#### Analysis

Time Complexity : V + E

Space Complexity : V + E


#### Code
Solution 1 : BFS
```java
/*
* class GraphNode {
*   public int key;
*   public List<GraphNode> neighbors;
*   public GraphNode(int key) {
*     this.key = key;
*     this.neighbors = new ArrayList<GraphNode>();
*   }
* }
*/
public class Solution {
  public List<GraphNode> copy(List<GraphNode> graph) {
    Map<GraphNode, GraphNode> hm = new HashMap<>();
    List<GraphNode> result = new ArrayList<>();
    for(GraphNode node : graph){
    	bfs(hm, result, node);
    }
    return result;
  }

  public void bfs(Map<GraphNode, GraphNode> hm, List<GraphNode> result, GraphNode node){
  	if(hm.containsKey(node)){
    	return;
    }
    Queue<GraphNode> queue = new ArrayDeque<>();
    GraphNode newNode = new GraphNode(node.key);
    Set<GraphNode> visited = new HashSet<>();
    hm.put(node, newNode);
    queue.offer(node);
    while(!queue.isEmpty()){
      GraphNode cur = queue.poll();
      if(visited.contains(cur)){
        continue;
      }
      GraphNode copyCur = hm.get(cur);
      for(GraphNode neighbor : cur.neighbors){
        queue.offer(neighbor);
        GraphNode copyNeighbor = new GraphNode(neighbor.key);
        hm.put(neighbor, copyNeighbor);
        copyCur.neighbors.add(copyNeighbor);
      }
      result.add(copyCur);
      visited.add(cur);
	  }
  }
}

```

Solution 2 : DFS

```java
/*
* class GraphNode {
*   public int key;
*   public List<GraphNode> neighbors;
*   public GraphNode(int key) {
*     this.key = key;
*     this.neighbors = new ArrayList<GraphNode>();
*   }
* }
*/
public class Solution {
  public List<GraphNode> copy(List<GraphNode> graph) {
    Map<GraphNode, GraphNode> hm = new HashMap<>();
    List<GraphNode> result = new ArrayList<>();
    for(GraphNode node : graph){
    	result.add(dfs(hm, node));
    }
    return result;
  }

  public GraphNode dfs(Map<GraphNode, GraphNode> hm, GraphNode node){
  	if(node == null){
  		return null;
  	}
  	if(hm.containsKey(node)){
    	return hm.get(node);
    }
    GraphNode newNode = new GraphNode(node.key);
    hm.put(node, newNode);
    for(GraphNode gn : node.neighbors){
    	newNode.neighbors.add(dfs(hm, gn));
    }
    return newNode;
  }
}

```
