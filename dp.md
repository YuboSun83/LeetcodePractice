## Dynamic Programming

## 1641. Count Sorted Vowel Strings
```java
class Solution {
    public int countVowelStrings(int n) {
        int[][] dp = new int[n + 1][5];
        for(int i = 0; i < n + 1; i++){
            for(int j = 0; j < 5; j++){
                if(i == 0 || j == 0) dp[i][j] = 1;
                else{
                    dp[i][j] = dp[i - 1][j] + dp[i][j - 1];
                }
            }
        }
        return dp[n][4];
    }
}
```

## 96. Unique Binary Search Trees
```java
class Solution {
    Integer[] memo;
    public int numTrees(int n) {
        memo = new Integer[n + 1];
        return dfs(n);
    }
    
    private int dfs(int n){
        if(n <= 1) return 1;
        if(memo[n] != null) return memo[n];
        
        int res = 0;
        for(int i = 1; i <= n; i++){
            int left = dfs(i - 1);
            int right = dfs(n - i);
            res += left * right;
        }
        
        memo[n] = res;
        return res;
    }
}
```
```java
class Solution {
    public int numTrees(int n) {
        int[] dp = new int[n + 1];
        dp[0] = dp[1] = 1;
        for(int i = 2; i <= n; i++){
            for(int j = 1; j <= i; j++){
                dp[i] += dp[j - 1] * dp[i - j];
            }
        }
        return dp[n];
    }
}
```

## 62. Unique Paths
```java
class Solution {
    public int uniquePaths(int m, int n) {
        int [][]dp = new int[m + 1][n + 1];
        dp[1][1] = 1;
        
        for(int i = 1; i <= m; i++){
            for(int j = 1; j <= n; j++){
                dp[i][j] += dp[i - 1][j] + dp[i][j -1];
            }
        }
        return dp[m][n];
    }
}
```


## 63. Unique Paths II
```java
class Solution {
    public int uniquePathsWithObstacles(int[][] obstacleGrid) {
        int m = obstacleGrid.length;
        int n = obstacleGrid[0].length;
        int[][] dp = new int [m + 1][n + 1];
        dp[1][1] = 1;
        
        for(int i = 1; i <= m; i++){
            for(int j = 1; j <= n; j++){
                if(obstacleGrid[i - 1][j - 1] == 1) dp[i][j] = 0;
                else dp[i][j] += dp[i - 1][j] + dp[i][j - 1];
            }
        }
        return dp[m][n];
    }
}
```

## 1143. Longest Common Subsequence
```java
class Solution {
    public int longestCommonSubsequence(String text1, String text2) {
        int m = text1.length();
        int n = text2.length();
        int[][] dp = new int[m + 1][n + 1];
        
        for(int i = 1; i <= m; i++){
            for(int j = 1; j <= n; j++){
                if(text1.charAt(i - 1) == text2.charAt(j - 1)){
                    dp[i][j] = dp[i - 1][j - 1] + 1;
                }else{
                    dp[i][j] = Math.max(dp[i][j - 1], dp[i - 1][j]);
                }
            }
        }
        return dp[m][n];
    }
}
```
