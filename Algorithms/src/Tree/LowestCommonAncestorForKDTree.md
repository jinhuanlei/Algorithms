## Lowest Common Ancestor For K DTree
Given two nodes in a K-nary tree, find their lowest common ancestor.

#### Assumptions

-There is no parent pointer for the nodes in the K-nary tree.

-The given two nodes are guaranteed to be in the K-nary tree.

#### Solution
遍历所有孩子 记录返回的Node 如果非Null的值为2， return root 如果是1 
返回那个Node， 剩下的返回null

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
    public KnaryTreeNode lowestCommonAncestor(KnaryTreeNode root, KnaryTreeNode a, KnaryTreeNode b) {
        if(root == null || root == a || root == b) {
            return root;
        }
        KnaryTreeNode result = null;
        int count = 0;
        for(KnaryTreeNode node : root.children){
        	KnaryTreeNode temp = lowestCommonAncestor(node, a, b);
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