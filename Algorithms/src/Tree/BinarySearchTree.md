## Binary Search Tree
#### Search in Binary Tree

```java
public class Solution {
  public TreeNode search(TreeNode root, int key) {
    // Write your solution here
    if(root == null){
      return null;
    }
    if(key < root.key){
      return search(root.left, key);
    }else if(key > root.key){
      return search(root.right, key);
    }
    return root;
  }
}
```


#### Insert in Binary Tree

```java
public class Solution {
  public TreeNode insert(TreeNode root, int key) {
    // Write your solution here
    if(root == null){
      return new TreeNode(key);
    }
    if(key < root.key){
      root.left = insert(root.left, key);
    }else if(key > root.key){
      root.right = insert(root.right, key);
    }
    return root;
  }
}

```


#### Delete in Binary Tree

```java
public class Solution {
  public TreeNode deleteTree(TreeNode root, int key) {
    // Write your solution here
    if(root == null){
      return root;
    }
    if(key < root.key){
      root.left = deleteTree(root.left, key);
      return root;
    }else if(key > root.key){
      root.right = deleteTree(root.right, key);
      return root;
    }

    // case 1 key == root.key
    if(root.left == null && root.right == null){
      return null;
    }else if(root.left == null){
      // case 2
      return root.right;
    }else if(root.right == null){
      // case 3
      return root.left;
    }

    // case 4.1
    if(root.right.left == null){
      root.right.left = root.left;
      return root.right;
    }

    // case 4.2
    TreeNode newNode = findSmallestLargerNode(root.right);
    newNode.left = root.left;
    newNode.right = root.right;
    return newNode;
  }

  public TreeNode findSmallestLargerNode(TreeNode root){
    TreeNode pre = null;
    TreeNode cur = root;
    while(cur.left != null){
      pre = cur;
      cur = cur.left;
    }
    pre.left = cur.right;
    return cur;
  }
}

```

