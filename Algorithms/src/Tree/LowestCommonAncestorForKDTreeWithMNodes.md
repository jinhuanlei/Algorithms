## Lowest Common Ancestor For KDTree With M Nodes
Given M nodes in a K-nary tree, find their lowest common ancestor.

#### Assumptions

- M >= 2.

- There is no parent pointer for the nodes in the K-nary tree.

- The given M nodes are guaranteed to be in the K-nary tree.
#### Examples

            5
    
          /   \
    
         9   12
    
       / | \      \
    
      1 2 3     14



The lowest common ancestor of 2, 3, 14 is 5.

The lowest common ancestor of 2, 3, 9 is 9.

#### Solution

结合LCA with KDTree and LCA with M nodes

```java
/**
* public class KnaryTreeNode {
 *     int key;
 *     List<KnaryTreeNode> children;
 *     public KnaryTreeNode(int key) {
 *         this.key = key;
 *         this.children = new ArrayList<>();
 *     }
 * }
 */
public class Solution {
  public KnaryTreeNode lowestCommonAncestor(KnaryTreeNode root, List<KnaryTreeNode> nodes) {
    if(root == null || nodes == null){
    	return null;
    }
    Set<KnaryTreeNode> hs = new HashSet<>();
    for(KnaryTreeNode node : nodes){
      hs.add(node);
    }
    return lowestCommonAncestorHelper(root, hs);
  }

  public KnaryTreeNode lowestCommonAncestorHelper(KnaryTreeNode root, Set<KnaryTreeNode> hs){
    if(root == null || hs.contains(root)){
      return root;
    }
  	KnaryTreeNode result = null;
    int count = 0;
    for(KnaryTreeNode node : root.children){
    	KnaryTreeNode temp = lowestCommonAncestorHelper(node, hs);
    	if(temp != null){
    		count++;
    		result = temp;
    		if(count == 2){
    			return root;
    		}
    	}
    }
    return result;
  }
}
```