## Tree Traversal (Iterative way)
Using iterative way will have Space Complexity of O(1). 
If the data set is too large, using the recursive way will cause Stack Over flow Exception.
### Pre Order

```java
public class Solution {
  public List<Integer> preOrder(TreeNode root) {
    // Write your solution here
    if(root == null){
        return new ArrayList<>();
    }
    List<Integer> result = new ArrayList<>();
    Deque<TreeNode> stack = new ArrayDeque<>();
    stack.offerFirst(root);
    while(!stack.isEmpty()){
        TreeNode cur = stack.pollFirst();
        result.add(cur.key);
        if(cur.right != null){
            stack.offerFirst(cur.right);
        }
        if(cur.left != null){
            stack.offerFirst(cur.left);
        }
    }
    return result;
  }
}

```

### In Order

```java
public class Solution {
  public List<Integer> inOrder(TreeNode root) {
    // Write your solution here
    if(root == null){
        return new ArrayList<Integer>();
    }
    List<Integer> result = new ArrayList<>();
    Deque<TreeNode> stack = new ArrayDeque<>();
    TreeNode helper = root;
    while(helper != null || !stack.isEmpty()){
        if(helper != null){
            stack.offerFirst(helper);
            helper = helper.left;
        }else{
            TreeNode cur = stack.pollFirst();
            result.add(cur.key);
            helper = cur.right;
        }
    }
    return result;
  }
}

```

### Post Order

* case 1 : pre is parent, cur node go down(left with high priority)
* case 2 : pre is cur.left. we go right, if right is null, print cur node
* case 3 : pre is cur.right, print cur node

```java
public class Solution {
  public List<Integer> postOrder(TreeNode root) {
    // Write your solution here
    if(root == null){
        return new ArrayList<Integer>();
    }
    Deque<TreeNode> stack = new ArrayDeque<>();
    List<Integer> result = new ArrayList<>();
    stack.offerFirst(root);
    TreeNode pre = null;
    while( !stack.isEmpty() ){
        TreeNode cur = stack.peekFirst();
        if(pre == null || pre.left == cur || pre.right == cur){
            // case1:  traverse down
            if(cur.left != null){
                stack.offerFirst(cur.left);
            }else if(cur.right != null){
                stack.offerFirst(cur.right);
            }else{
                result.add(cur.key);
                stack.pollFirst();
            }
        }else if(pre == cur.left){
            // case2: go right
            if(cur.right != null){
                stack.offerFirst(cur.right);
            }else{
                result.add(cur.key);
                stack.pollFirst();
            }
        }else{
            // case3
            result.add(cur.key);
            stack.pollFirst();

        }
        pre = cur;
    }
    return result;
  }
}

```
