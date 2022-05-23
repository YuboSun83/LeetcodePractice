## Breadth-First Search

## 102. Binary Tree Level Order Traversal
```java
// must save size before poll/offer into queue cuz size is dynamic.
class Solution {
    public List<List<Integer>> levelOrder(TreeNode root) {
        List<List<Integer>> res = new LinkedList<>();
        
        if(root == null) return res;
        
        Queue<TreeNode> queue = new LinkedList<>();
        queue.offer(root);
        
        while(!queue.isEmpty()){
            int size = queue.size();
            List<Integer> ans = new LinkedList<>();
            for(int i = 0; i < size; i++){
                TreeNode cur = queue.poll();
                ans.add(cur.val);
                if(cur.left != null) queue.offer(cur.left);
                if(cur.right != null) queue.offer(cur.right);
            }
            res.add(ans);
        }
        return res;
    }
}
```

## 104. Maximum Depth of Binary Tree
```java
class Solution {
    public int maxDepth(TreeNode root) {
        int res = 0;
        if(root == null) return res;
        Queue<TreeNode> q = new LinkedList<>();
        q.offer(root);
        
        while(!q.isEmpty()){
            int size = q.size();
            for(int i = 0; i < size; i++){
                TreeNode cur = q.poll();
                if(cur.left != null) q.offer(cur.left);
                if(cur.right != null) q.offer(cur.right);
            }
            res++;
        }
        return res;
    }
}
```

## 107. Binary Tree Level Order Traversal II
```java
class Solution {
    public List<List<Integer>> levelOrderBottom(TreeNode root) {
        List<List<Integer>> res = new LinkedList<>();
        if(root == null) return res;
        
        Queue<TreeNode> q = new LinkedList<>();
        q.offer(root);
        while(!q.isEmpty()){
            int size = q.size();
            List<Integer> ans = new LinkedList<>();
            for(int i =0; i < size; i++){
                TreeNode cur = q.poll();
                if(cur.left != null) q.offer(cur.left);
                if(cur.right != null) q.offer(cur.right);
                ans.add(cur.val);
            }
            res.add(0, ans);
        }
        return res;
    }
}
```

## 111. Minimum Depth of Binary Tree
```java
class Solution {
    public int minDepth(TreeNode root) {
        if(root == null) return 0;
        int res = 1;
        Queue<TreeNode> q = new LinkedList<>();
        q.offer(root);
        while(!q.isEmpty()){
            int size = q.size();
            for(int i = 0; i < size; i++){
                TreeNode cur = q.poll();
                if(cur.left == null && cur.right == null) return res;
                else{
                    if(cur.left != null) q.offer(cur.left);
                    if(cur.right != null) q.offer(cur.right);
                }
            }
            res++;
        }
        return res;
    }
}
```

### 117. Populating Next Right Pointers in Each Node II
Given a binary tree
```java
struct Node {
  int val;
  Node *left;
  Node *right;
  Node *next;
}
```
Populate each next pointer to point to its next right node. If there is no next right node, the next pointer should be set to NULL.

Initially, all next pointers are set to NULL.
```java
class Solution {
    public Node connect(Node root) {
        if(root == null) return root;
        Queue<Node> q = new LinkedList<>();
        q.add(root);
        
        while(!q.isEmpty()){
            int s = q.size();
            Node pre = null;
            Node cur = null;
            for(int i = 0; i < s; i++){
                pre = cur;
                cur = q.poll();
                if(pre != null) pre.next = cur;
                if(cur.left != null) q.offer(cur.left);
                if(cur.right != null) q.offer(cur.right);
            }
        }
        return root;
    }
}
```