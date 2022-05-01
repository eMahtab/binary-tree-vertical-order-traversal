# Binary Tree Vertical Order Traversal
## https://leetcode.com/problems/binary-tree-vertical-order-traversal
## https://www.lintcode.com/problem/651

Given a binary tree, return the vertical order traversal of its nodes' values. (ie, from top to bottom, column by column).

#### Very Important 😯: If two nodes are in the same row and column, the order should be from left to right.

![Binary Tree Vertical Order Traversal](vertical-order-traversal.JPG?raw=true "Binary Tree Vertical Order Traversal")

```
Examples 1:

Input: [3,9,20,null,null,15,7]

   3
  /\
 /  \
 9  20
    /\
   /  \
  15   7 

Output:

[
  [9],
  [3,15],
  [20],
  [7]
]
Examples 2:

Input: [3,9,8,4,0,1,7]

     3
    /\
   /  \
   9   8
  /\  /\
 /  \/  \
 4  01   7 

Output:

[
  [4],
  [9],
  [3,0,1],
  [8],
  [7]
]
Examples 3:

Input: [3,9,8,4,0,1,7,null,null,null,2,5] (0's right child is 2 and 1's left child is 5)

     3
    /\
   /  \
   9   8
  /\  /\
 /  \/  \
 4  01   7
    /\
   /  \
   5   2

Output:

[
  [4],
  [9,5],
  [3,0,1],
  [8,2],
  [7]
]
```

# Implementation :
```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 *     TreeNode(int val, TreeNode left, TreeNode right) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
class Solution {
    class Node {
        TreeNode treeNode;
        int horizontalDistance;
        Node(TreeNode treeNode, int horizontalDistance) {
            this.treeNode = treeNode;
            this.horizontalDistance = horizontalDistance;
        } 
    }
    
    public List<List<Integer>> verticalOrder(TreeNode root) {
        List<List<Integer>> res = new ArrayList<>();
        if(root == null) return res;
        Queue<Node> q = new LinkedList<>();
        q.offer(new Node(root,0));
        Map<Integer,List<Integer>> map = new HashMap<>();
        int min = Integer.MAX_VALUE, max = Integer.MIN_VALUE;
        while(!q.isEmpty()) {
            Node current = q.poll();
            List<Integer> list = map.getOrDefault(current.horizontalDistance, new ArrayList<Integer>());
            list.add(current.treeNode.val);
            map.put(current.horizontalDistance,list);
            min = Math.min(min, current.horizontalDistance);
            max = Math.max(max, current.horizontalDistance);
            if(current.treeNode.left != null)
                q.offer(new Node(current.treeNode.left, current.horizontalDistance - 1));
            if(current.treeNode.right != null)
                q.offer(new Node(current.treeNode.right, current.horizontalDistance + 1));
        }
        for(int i = min; i <= max; i++) {
            res.add(map.get(i));
        }
       return res; 
    }
}
```

# References :
https://www.youtube.com/watch?v=QWbVCqIhTO4
