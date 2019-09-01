### 1. Reconstruct Binary Tree With Preorder And Inorder
Given the preorder and inorder traversal sequence of a binary tree, reconstruct the original tree.

#### Assumptions

The given sequences are not null and they have the same length
There are no duplicate keys in the binary tree
Examples

preorder traversal = {5, 3, 1, 4, 8, 11}

inorder traversal = {1, 3, 4, 5, 8, 11}

the corresponding binary tree is

            5
    
          /    \
    
        3        8
    
      /   \        \
    
    1      4        11

How is the binary tree represented?

We use the pre order traversal sequence with a special symbol "#" denoting the null node.

For Example:

The sequence [1, 2, #, 3, 4, #, #, #] represents the following binary tree:

        1
    
      /   \
    
     2     3
    
          /
    
        4
        
        
#### Solution

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
  public TreeNode reconstruct(int[] inOrder, int[] preOrder) {
    Map<Integer , Integer> hashMap = new HashMap<>();
    for(int x = 0; x < inOrder.length; x++){
    	hashMap.put(inOrder[x], x);
    }
    return reconstructHelper(0, inOrder.length - 1, preOrder, 0, preOrder.length - 1, hashMap);
  }

  public TreeNode reconstructHelper(int inLeft, int inRight, int[] preOrder, int preLeft, int preRight, Map<Integer, Integer> hashMap){
  	if(inLeft > inRight){
  		return null;
  	}
  	TreeNode root = new TreeNode(preOrder[preLeft]);
  	int leftSize = hashMap.get(root.key) - inLeft;
  	root.left = reconstructHelper(inLeft, inLeft + leftSize - 1, preOrder, preLeft + 1, preLeft + leftSize, hashMap);
  	root.right = reconstructHelper(inLeft + leftSize + 1, inRight, preOrder, preLeft + leftSize + 1, preRight, hashMap);
  	return root;
  }
}

```

### 1. Reconstruct BST With PostOrder

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
  public TreeNode reconstruct(int[] post) {
    int[] inOrder = new int[post.length];
    for(int x = 0; x < post.length; x++){
      inOrder[x] = post[x];
    }
    Arrays.sort(inOrder);
    Map<Integer , Integer> hashMap = new HashMap<>();
    for(int x = 0; x < inOrder.length; x++){
      hashMap.put(inOrder[x], x);
    }
    return reconstructHelper(hashMap, 0, inOrder.length - 1, post, 0, post.length - 1);
  }

  public TreeNode reconstructHelper(Map<Integer, Integer> hashMap, int inLeft, int inRight, int[] postOrder, int postLeft, int postRight){
    if(inLeft > inRight){
      return null;
    }
    TreeNode root = new TreeNode(postOrder[postRight]);
    int mid = hashMap.get(root.key);
    int leftSize = mid - inLeft;
    root.left = reconstructHelper(hashMap, inLeft, mid - 1, postOrder, postLeft, postLeft + leftSize - 1);
    root.right = reconstructHelper(hashMap, mid + 1, inRight, postOrder, postLeft + leftSize, postRight - 1);
    return root;
  }
}

```




