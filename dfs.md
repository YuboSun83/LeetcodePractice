## Depth first search

## 144. Binary Tree Preorder Traversal
```java
class Solution {
    public List<Integer> preorderTraversal(TreeNode root) {
        List<Integer> res = new ArrayList<>();
        preorderHelper(root, res);
        return res;
    }
    
    private void preorderHelper(TreeNode root, List<Integer> res){
        if(root == null) return;
        res.add(root.val);
        preorderHelper(root.left, res);
        preorderHelper(root.right, res);
    }
}
```

## 94. Binary Tree Inorder Traversal
```java
class Solution {
    public List<Integer> inorderTraversal(TreeNode root) {
        List<Integer> res = new ArrayList<>();
        inorderTraversalHelper(root, res);
        return res;
    }
    private void inorderTraversalHelper(TreeNode root, List<Integer> res){
        if(root == null) return;
        inorderTraversalHelper(root.left, res);
        res.add(root.val);
        inorderTraversalHelper(root.right, res);
    }
}
```

## 145. Binary Tree Postorder Traversal
```java
class Solution {
    public List<Integer> postorderTraversal(TreeNode root) {
        List<Integer> res = new ArrayList<>();
        postorderTraversalHelper(root, res);
        return res;
    }
    
    private void postorderTraversalHelper(TreeNode root, List<Integer> res){
        if(root == null) return;
        postorderTraversalHelper(root.left, res);
        postorderTraversalHelper(root.right, res);
        res.add(root.val);
    }
}
```

## 104. Maximum Depth of Binary Tree
```java
class Solution {
    public int maxDepth(TreeNode root) {
        if(root == null) return 0;
        return 1 + Math.max(maxDepth(root.left), maxDepth(root.right));
    }
}
```

## 124. Binary Tree Maximum Path Sum
```java
class Solution {    
    public int maxPathSum(TreeNode root) {
        int max = Integer.MIN_VALUE;
        dfs(root, max);
        return max;
    }
    private void dfs(TreeNode root, int max){
        if(root == null) return 0;
        int left = dfs(root.left);
        int right = dfs(root.right);
        
        left = left > 0 ? left : 0;
        right = right > 0 ? right : 0;
        
        max = Math.max(max, left + right + root.val);
    }
}
```

## 129. Sum Root to Leaf Numbers
```java
class Solution {
    int sum = 0;
    public int sumNumbers(TreeNode root) {
        if(root == null) return 0;
        dfs(root, 0);
        return sum;
    }
    
    private void dfs(TreeNode root, int num){
        num = num * 10 + root.val;
        if(root.left == null && root.right == null){
            sum += num;
            return;
        }
        if(root.left != null){
            dfs(root.left, num);
        }
        if(root.right != null){
            dfs(root.right, num);
        }
    }
}
```