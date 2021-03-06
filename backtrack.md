## BackTrack
## 46. Permutations
```java
class Solution {
    public List<List<Integer>> permute(int[] nums) {
        List<List<Integer>> res = new ArrayList<>();
        dfs(res, nums, 0);
        return res;
    }
    
    private void dfs(List<List<Integer>> res, int[] nums, int index){
        if(index == nums.length){
            List<Integer> ans = new ArrayList<>();
            for(int i = 0; i < nums.length; i++){
                ans.add(nums[i]);
            }
            res.add(ans);
            return;
        }
        
        for(int i = index; i < nums.length; i++){
            swap(nums, index, i);
            dfs(res, nums, index + 1);
            swap(nums, index, i);
        }
    }
    
    private void swap(int[] nums, int i, int j){
        int tmp = nums[i];
        nums[i] = nums[j];
        nums[j] = tmp;
    }
}
```

## 47. Permutations II
```java
class Solution {
    public List<List<Integer>> permuteUnique(int[] nums) {
        List<List<Integer>> res = new ArrayList<>();
        permutation(res, nums, 0);
        return res;
    }
    
    private void swap(int[] nums, int i, int j){
        int tmp = nums[i];
        nums[i] = nums[j];
        nums[j] = tmp;
    }
    
    private void permutation(List<List<Integer>> res, int[] nums, int index){
        if(index == nums.length){
            List<Integer> ans = new ArrayList<>();
            for(int i = 0; i < nums.length; i++){
                ans.add(nums[i]);
            }
            res.add(ans);
            return;
        }
        
        Set<Integer> visited = new HashSet<>();
        for(int i = index; i < nums.length; i++){
            swap(nums, index, i);
            if(visited.add(nums[index])){
                permutation(res, nums, index + 1);
            }
            swap(nums, index, i);
        }
    }
}
```

## 17. Letter Combinations of a Phone Number
```java
class Solution {
    public List<String> letterCombinations(String digits) {
        List<String> list = new ArrayList<>();
        if(digits.length() == 0) return list;
        String[] dict = new String[] {"", "", "abc", "def", "ghi", "jkl", "mno", "pqrs", "tuv", "wxyz" };
        backtrack(list, "", digits, dict, 0);
        return list;
    }
    
    private void backtrack(List<String> list, String s, String digits, String[] dict, int start){
        if(s.length() >= digits.length()){
            list.add(s);
            return;
        }
        for(int i = start; i < digits.length(); i++){
            int tmp = digits.charAt(i) - '0';
            for(int j = 0; j < dict[tmp].length(); j++){
                s += dict[tmp].charAt(j);
                backtrack(list, s, digits, dict, i + 1);
                s = s.substring(0, s.length() - 1);
            }
        }
    }
}
```

## 216. Combination Sum III
```java
class Solution {
    public List<List<Integer>> combinationSum3(int k, int n) {
        List<List<Integer>> res = new ArrayList<>();
        backtrack(res,  new ArrayList<Integer>(), k, 1, n);
        return res;
    }
    
    private void backtrack(List<List<Integer>> res, List<Integer> comb, int k, int start, int n){
        if(comb.size() == k && n == 0){
            List<Integer> ans = new ArrayList<Integer>(comb);
            res.add(ans);
            return;
        }
        
        for(int i = start; i <= 9; i++){
            comb.add(i);
            backtrack(res, comb, k, i + 1, n - i);
            comb.remove(comb.size() - 1);
        }
    }
}
```

## 78. Subsets
```java
class Solution {
    public List<List<Integer>> subsets(int[] nums) {
        List<List<Integer>> res = new ArrayList<>();
        dfs(res, nums, new ArrayList<Integer>(), 0);
        return res;
    }
    
    private void dfs(List<List<Integer>> res, int[] nums, List<Integer> ans, int index){
        if(index >= nums.length){
            res.add(new ArrayList<Integer>(ans));
            return;
        }
        
        ans.add(nums[index]);
        dfs(res, nums, ans, index + 1);
        ans.remove(ans.size() - 1);
        
        dfs(res, nums, ans, index + 1);
    }
}
```