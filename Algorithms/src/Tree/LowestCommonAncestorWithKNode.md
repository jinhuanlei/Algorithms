## Lowest Common Ancestor with K Node
Given K nodes in a binary tree, find their lowest common ancestor.

#### Assumptions

K >= 2

There is no parent pointer for the nodes in the binary tree

The given K nodes are guaranteed to be in the binary tree

#### Examples

            5
    
          /   \
    
         9     12
    
       /  \      \
    
      2    3      14

The lowest common ancestor of 2, 3, 14 is 5

The lowest common ancestor of 2, 3, 9 is 9

## Solution

solution 1 : 
和解决普通LCA一样

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
  public TreeNode lowestCommonAncestor(TreeNode root, List<TreeNode> nodes) {
    if(root == null || nodes == null){
    	return null;
    }
    Set<TreeNode> hs = new HashSet<>();
    for(TreeNode node : nodes){
    	hs.add(node);
    }
    return lowestCommonAncestorHelper(root, hs);
  }

  public TreeNode lowestCommonAncestorHelper(TreeNode root, Set<TreeNode> hs){
  	if(root == null || hs.contains(root)){
  		return root;
  	}
  	TreeNode left = lowestCommonAncestorHelper(root.left, hs);
  	TreeNode right = lowestCommonAncestorHelper(root.right, hs);
  	if(left != null && right != null){
  		return root;
  	}
  	return left == null ? right : left;
  }
}
```