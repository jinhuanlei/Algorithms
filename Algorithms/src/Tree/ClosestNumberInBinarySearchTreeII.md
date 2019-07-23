## Closest Number In Binary Search Tree II
In a binary search tree, find k nodes containing the closest numbers to the given target number. return them in sorted array

#### Assumptions:

The given root is not null.
There are no duplicate keys in the binary search tree.
Examples:

        5
    
      /    \
    
    2      11
    
         /    \
    
        6     14

closest number to 4 is 5

closest number to 10 is 11

closest number to 6 is 6

How is the binary tree represented?

We use the level order traversal sequence with a special symbol "#" denoting the null node.

#### Example:

The sequence [1, 2, 3, #, #, 4] represents the following binary tree:

        1
    
      /   \
    
     2     3
    
          /
    
        4

#### Code
**Solution 1 :**

Step 1 : inorder to a sorted list

Step 2 : find a closest Node

Step 3 : 中心开花

Time : N + K
Space : N

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
  public int[] closestKValues(TreeNode root, double target, int k) {
    if(k == 1){
      return new int[]{root.key};
    }
    List<Integer> values = new ArrayList<Integer>();
    // N
    inOrder(values, root);
    // logN
    int closestIndex = findClosest(values, target);
    // [left, right]
    int left = closestIndex;
    int right = closestIndex;
    for(int x = 1; x < k; x++){
    	if(left <= 0 && right >= values.size() - 1){
    		break;
    	}else if(left <= 0){
    		right++;
    	}else if(right >= values.size() - 1){
    		left--;
    	}else{
    		double leftVal = Math.abs(target - (double)values.get(left - 1));
    		double rightVal = Math.abs(target - (double)values.get(right + 1));
    		if(leftVal <= rightVal){
    			left--;
    		}else{
    			right++;
    		}
    	}
    }
    int size = k > values.size() ? values.size() : k;
    int[] result = new int[size];
    int index = 0;
    for(int x = left; x <= right; x++){
		  result[index++] = values.get(x);
    }
    return result;
  }

  public int findClosest(List<Integer> values, double target){
  	int left = 0;
  	int right = values.size() - 1;
  	while(left < right - 1){
  		int mid = left + (right - left) / 2;
  		if(values.get(mid) > target){
  			right = mid;
  		}else if(values.get(mid) < target){
  			left = mid;
  		}else{
  			return mid;
  		}
  	}
  	// post processing
  	double leftVal = Math.abs(target - (double)values.get(left));
    double rightVal = Math.abs(target - (double)values.get(right));
    if(leftVal < rightVal){
      return left;
    }else{
      return right;
    }
  }

  public void inOrder(List<Integer> values, TreeNode root){
  	if(root == null){
  		return;
  	}
  	inOrder(values, root.left);
	  values.add(root.key);
  	inOrder(values, root.right);
  }
}
```

**Solution 2 :**
Step 1 : Use a Queue as a Sliding Window

Step 2 : In order traverse, 

Case 1 : enqueue if size < k

Case 2 : if abs( X - target ) < abs(deque.left - target), we poll left and insert X at right side

Case 3 : return

Time : N
Space : K

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
  public int[] closestKValues(TreeNode root, double target, int k) {
    Queue<Integer> queue = new ArrayDeque<>();
    closestKValuesHelper(root, queue, target, k);
    int[] result = new int[queue.size()];
    for(int x = 0; x < result.length; x++){
    	result[x] = queue.poll();
    }
    return result;
  }

  public void closestKValuesHelper(TreeNode root, Queue<Integer> queue , double target, int k){
    if(root == null){
    	return;
    }
    closestKValuesHelper(root.left, queue, target, k);
    if(queue.size() < k){
    	queue.offer(root.key);
    }else{
    	int top = queue.peek();
    	double left = Math.abs(target - top);
    	double right = Math.abs(target - root.key);
    	if(right < left){
    		queue.poll();
    		queue.offer(root.key);
    	}
    }
    closestKValuesHelper(root.right, queue, target, k);
  }
}

```