Given a binary tree in which each node contains an integer number. 

Determine if there exists a path (the path can only be from one node to itself or to any of its descendants), the sum of the numbers on the path is the given target number.

Examples
```
    5

  /    \

2      11

     /    \

    6     14

  /

 3
```

If target = 17, There exists a path 11 + 6, the sum of the path is target.

If target = 20, There exists a path 11 + 6 + 3, the sum of the path is target.

If target = 10, There does not exist any paths sum of which is target.

If target = 11, There exists a path only containing the node 11.

How is the binary tree represented?

We use the level order traversal sequence with a special symbol "#" denoting the null node.

For Example:

The sequence [1, 2, 3, #, #, 4] represents the following binary tree:
```
    1

  /   \

 2     3

      /

    4
```

Solution 

要maintain一个List, 来记录path, 然后从后往前计算当path等于target的时候 return true

Time: O(N)
Space: O(N)

```java
/**
 * public class TreeNode {
 *   public int key;
 *   public TreeNode left;
 *   public TreeNode right;
 *   public TreeNode(int key) {
 *     this.key = key;
 *   }
 * }
 */
public class Solution {
  public boolean exist(TreeNode root, int target) {
    List<Integer> path = new ArrayList<>();
    return existHelper(root, target, path);
  }

  public boolean existHelper(TreeNode root, int target, List<Integer> path){
    if(root == null){
      return false;
    }
    path.add(root.key);
    int sum = 0;
    for(int x = path.size() - 1; x >= 0; x--){
      sum += path.get(x);
      if(sum == target){
        return true;
      }
    }
    if(existHelper(root.left, target, path) || existHelper(root.right, target, path)){
      return true;
    }
    path.remove(path.size() - 1);
    return false;
  }
}

```