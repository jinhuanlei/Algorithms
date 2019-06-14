## Bipartite

Determine if an undirected graph is bipartite. A bipartite graph is one in which the nodes can be divided into two groups such that no nodes have direct edges to other nodes in the same group.

Examples
```
1  --   2

    /

3  --   4
```


is bipartite (1, 3 in group 1 and 2, 4 in group 2).
```
1  --   2

    /   |

3  --   4
```


is not bipartite.

### Idea
Step1 : 给第一个点染色, 然后使用BFS逐层染色两两点之间颜色需要不一样. 如果有冲突说明不是Bipartite.

Step2 : 考虑图不一定是全连接的需要遍历所有点, 每个点做一个BFS. 这里可以用visited记录访问过的点

### Analysis

Space : visited HashMap  O(V)

Time : O(V + E) 访问所有 Node 和 Edge

###  Code:
```java
/**
 * public class GraphNode {
 *   public int key;
 *   public List<GraphNode> neighbors;
 *   public GraphNode(int key) {
 *     this.key = key;
 *     this.neighbors = new ArrayList<GraphNode>();
 *   }
 * }
 */
public class Solution {
  public boolean isBipartite(List<GraphNode> graph) {
    // write your solution here
    Map<GraphNode, Integer> visited = new HashMap<>();
    for(GraphNode node : graph){
      if(!bfs(node, visited)){
        return false;
      }
    }
    return true;
  }

  public boolean bfs(GraphNode root, Map<GraphNode, Integer> visited){
    if(visited.containsKey(root)){
      return true;
    }
    Queue<GraphNode> queue = new ArrayDeque<>();
    visited.put(root, 0);
    queue.offer(root);
    while(!queue.isEmpty()){
      GraphNode cur = queue.poll();
      int curGroup = visited.get(cur);
      int neighborGroup = curGroup == 1 ? 0 : 1;
      for(GraphNode neighbor : cur.neighbors){
        if(!visited.containsKey(neighbor)){
          queue.offer(neighbor);
          visited.put(neighbor, neighborGroup);
        }else if(visited.get(neighbor) != neighborGroup){
          return false;
        }
      }
    }
    return true;
  }
}
```