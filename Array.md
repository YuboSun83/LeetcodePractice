### EASY 
189.Rotate Array
88.Merge Sorted Array
1260.Shift 2D Grid
941.Valid Mountain Array
283.Move Zeros
167.Two Sum II – Input array is sorted
26.Remove Duplicates from Sorted Array
### MEDIUM 
80.Remove Duplicates from Sorted Array II
56.Merge Intervals
11.Container With Most Water
31.Next Permuation
442.Find All Duplicates in an Array
48.Rotate Image
75.Sort Colors
57.Insert Interval
### HARD 
42.Trapping Rain Water

### 189.Rotate Array
Given an array, rotate the array to the right by k steps, where k is non-negative.
```java
// use more space to create a new array to contain
class Solution {
    public void rotate(int[] nums, int k) {
        if(nums.length <= 1) return;
        int[] tmp = new int[nums.length];
        int l = k % nums.length;
        
        for(int i = 0; i < nums.length; i++){
            tmp[i] = nums[(i + nums.length - l) % nums.length];
            // System.out.println(tmp[i]);
        }
        
        for(int j = 0; j < nums.length; j++){
            nums[j] = tmp[j];
        }
    }
}
```
```java
// 3 step reverse
class Solution {
    public void rotate(int[] nums, int k) {
        if(nums.length <= 1) return;
        int l = k % nums.length;
        reverse(nums, 0, nums.length -1);
        reverse(nums, 0, l - 1);
        reverse(nums, l, nums.length -1);
    }
    
    private void reverse(int[] nums, int start, int end){
        while(start < end){
            swap(nums, start, end);
            start ++;
            end --;
        }
    }
    
    private void swap(int [] nums, int i, int j){
        int tmp = nums[i];
        nums[i] = nums[j];
        nums[j] = tmp;
    }
}
```

### 88.Merge Sorted Array
You are given two integer arrays nums1 and nums2, sorted in non-decreasing order, and two integers m and n, representing the number of elements in nums1 and nums2 respectively.

Merge nums1 and nums2 into a single array sorted in non-decreasing order.

The final sorted array should not be returned by the function, but instead be stored inside the array nums1. To accommodate this, nums1 has a length of m + n, where the first m elements denote the elements that should be merged, and the last n elements are set to 0 and should be ignored. nums2 has a length of n.

```java
// brute force
class Solution {
    public void merge(int[] nums1, int m, int[] nums2, int n) {
        if(n == 0) return;
        for(int i = 0; i < nums1.length; i ++){
            if(i >= m){
                for(int j = 0; j < n; j ++){
                    nums1[i] = nums2[j];
                    i++;
                }
            }
        }
        Arrays.sort(nums1);
    }
}
```
```java
// sort without Arrays.sort
class Solution {
    public void merge(int[] nums1, int m, int[] nums2, int n) {
        int l1 = m - 1,
            l2 = n - 1,
            l3 = m + n - 1;
        
        while(l1 >= 0 && l2 >= 0){
            nums1[l3--] = nums1[l1] > nums2[l2] ? nums1[l1 --] : nums2[l2 --];
        }
        
        while(l2 >= 0){
            nums1[l3 --] = nums2[l2 --];
        }
    }
}
```

### 1260.Shift 2D Grid
Given a 2D grid of size m x n and an integer k. You need to shift the grid k times.

In one shift operation:

Element at grid[i][j] moves to grid[i][j + 1].
Element at grid[i][n - 1] moves to grid[i + 1][0].
Element at grid[m - 1][n - 1] moves to grid[0][0].
Return the 2D grid after applying shift operation k times.
```java
// brute force to find new position
class Solution {
    public List<List<Integer>> shiftGrid(int[][] grid, int k) {
        List<List<Integer>> res = new ArrayList<>();
        int row = grid.length;
        int col = grid[0].length;
        for(int i = 0; i < row; i++){
            res.add(new ArrayList<Integer>());
        }
        k %= row * col;
        int d = row * col;
        int begin = d - k;
        int x = 0;
        for(int i = begin; i < d + begin; i++){
            int r = (i / col) % row;
            int c = i % col;
            res.get(x / col).add(grid[r][c]);
            x ++;
        }
        return res;
    }
}
```

### 941.Valid Mountain Array
Given an array of integers arr, return true if and only if it is a valid mountain array.

Recall that arr is a mountain array if and only if:

arr.length >= 3
There exists some i with 0 < i < arr.length - 1 such that:
arr[0] < arr[1] < ... < arr[i - 1] < arr[i]
arr[i] > arr[i + 1] > ... > arr[arr.length - 1]
```java
// two pointer, assume to people climb the mountain and go to peak. return true if they finally meet.
class Solution {
    public boolean validMountainArray(int[] arr) {
        if(arr.length < 3) return false;
        int left = 0;
        int right = arr.length - 1;
        while(left + 1 < arr.length - 1 && arr[left] < arr[left + 1]) left++;
        while(right - 1 > 0 && arr[right] < arr[right - 1]) right --;
        
        return left == right;
    }
}
```

### 283.Move Zeros
Given an integer array nums, move all 0's to the end of it while maintaining the relative order of the non-zero elements.

Note that you must do this in-place without making a copy of the array.
```java
// two pointers
class Solution {
    public void moveZeroes(int[] nums) {
        if(nums.length <= 1 || nums == null) return;
        int j = 0;
        for(int i = 0; i < nums.length; i++){
            if(nums[i] != 0){
                swap(nums, i, j);
                j++;
            }
        }
    }
    private void swap(int[] nums, int i, int j){
        int tmp = nums[i];
        nums[i] = nums[j];
        nums[j] = tmp;
    }
}
```

### 167.Two Sum II – Input array is sorted
Given a 1-indexed array of integers numbers that is already sorted in non-decreasing order, find two numbers such that they add up to a specific target number. Let these two numbers be numbers[index1] and numbers[index2] where 1 <= index1 < index2 <= numbers.length.

Return the indices of the two numbers, index1 and index2, added by one as an integer array [index1, index2] of length 2.

The tests are generated such that there is exactly one solution. You may not use the same element twice.

Your solution must use only constant extra space.
```java
// two pointers
class Solution {
    public int[] twoSum(int[] numbers, int target) {
        int left = 0;
        int right = numbers.length - 1;
        while(numbers[left] + numbers[right] != target){
            if(numbers[left] + numbers[right] > target) right --;
            else left ++;
        }
        
        return new int[]{left + 1, right + 1};
    }
}
```

### 26.Remove Duplicates from Sorted Array
Given an integer array nums sorted in non-decreasing order, remove the duplicates in-place such that each unique element appears only once. The relative order of the elements should be kept the same.

Since it is impossible to change the length of the array in some languages, you must instead have the result be placed in the first part of the array nums. More formally, if there are k elements after removing the duplicates, then the first k elements of nums should hold the final result. It does not matter what you leave beyond the first k elements.

Return k after placing the final result in the first k slots of nums.

Do not allocate extra space for another array. You must do this by modifying the input array in-place with O(1) extra memory.
```java
// two pointers
class Solution {
    public int removeDuplicates(int[] nums) {
        int result = 0;
        for(int n : nums){
            if(result == 0 || n > nums[result - 1]) nums[result++] = n;
        }
        return result;
    }
}
```

### 80.Remove Duplicates from Sorted Array II
Given an integer array nums sorted in non-decreasing order, remove some duplicates in-place such that each unique element appears at most twice. The relative order of the elements should be kept the same.

Since it is impossible to change the length of the array in some languages, you must instead have the result be placed in the first part of the array nums. More formally, if there are k elements after removing the duplicates, then the first k elements of nums should hold the final result. It does not matter what you leave beyond the first k elements.

Return k after placing the final result in the first k slots of nums.

Do not allocate extra space for another array. You must do this by modifying the input array in-place with O(1) extra memory.
```java
class Solution {
    public int removeDuplicates(int[] nums) {
       int i = 0;
       for (int n : nums)
          if (i < 2 || n > nums[i - 2])
             nums[i++] = n;
       return i;
    }
}
```

### 56.Merge Intervals
Given an array of intervals where intervals[i] = [starti, endi], merge all overlapping intervals, and return an array of the non-overlapping intervals that cover all the intervals in the input.
```java
class Solution {
    public int[][] merge(int[][] intervals) {
        if(intervals.length == 0 || intervals == null) return intervals;
        
        Arrays.sort(intervals, (a, b) -> Integer.compare(a[0], b[0]));
        LinkedList<int[]> merged = new LinkedList<>();
        for(int []curr : intervals){
            if(merged.isEmpty() || merged.getLast()[1] < curr[0])
                merged.add(curr);
            else{
                merged.getLast()[1] = Math.max(merged.getLast()[1], curr[1]);
            }
        }
        return merged.toArray(new int[0][]);
    }
}
```

### 11.Container With Most Water
You are given an integer array height of length n. There are n vertical lines drawn such that the two endpoints of the ith line are (i, 0) and (i, height[i]).

Find two lines that together with the x-axis form a container, such that the container contains the most water.

Return the maximum amount of water a container can store.

Notice that you may not slant the container.

```java
class Solution {
    public int maxArea(int[] height) {
        int left = 0;
        int right = height.length - 1;
        int res = 0;
        
        while(left < right){
            int w = right - left;
            int h = Math.min(height[left], height[right]);
            res = Math.max(res, w * h);
            if(height[left] < height[right]) left++;
            else if(height[left] > height[right]) right --;
            else{
                left++;
                right--;
            }
        }
        
        return res;
    }
}
```

### 31.Next Permuation
A permutation of an array of integers is an arrangement of its members into a sequence or linear order.

For example, for arr = [1,2,3], the following are considered permutations of arr: [1,2,3], [1,3,2], [3,1,2], [2,3,1].
The next permutation of an array of integers is the next lexicographically greater permutation of its integer. More formally, if all the permutations of the array are sorted in one container according to their lexicographical order, then the next permutation of that array is the permutation that follows it in the sorted container. If such arrangement is not possible, the array must be rearranged as the lowest possible order (i.e., sorted in ascending order).

For example, the next permutation of arr = [1,2,3] is [1,3,2].
Similarly, the next permutation of arr = [2,3,1] is [3,1,2].
While the next permutation of arr = [3,2,1] is [1,2,3] because [3,2,1] does not have a lexicographical larger rearrangement.
Given an array of integers nums, find the next permutation of nums.

The replacement must be in place and use only constant extra memory.

```java
class Solution {
    public void nextPermutation(int[] nums) {
        int p = findFirstDec(nums) - 1;
        if(p != -1){
            int l = findNextBigger(nums, nums[p]);
            swap(nums, p, l);
        }
        reverse(nums, p + 1);
    }
    
    private int findNextBigger(int[] nums, int p){
        for(int i = nums.length - 1; i >= 0; i--){
            if(nums[i] > p) return i;
        }
        return -1;
    }
    
    private int findFirstDec(int[] nums){
        for(int i = nums.length - 1; i > 0; i --){
            if(nums[i] > nums[i - 1]) return i;
        }
        return 0;
    }
    
    private void swap(int[] nums, int i, int j){
        int tmp = nums[i];
        nums[i] = nums[j];
        nums[j] = tmp;
    }
    
    private void reverse(int[] nums, int start){
        int end = nums.length - 1;
        while(start < end){
            swap(nums, start, end);
            start ++;
            end --;
        }
    }
}
```

### 442.Find All Duplicates in an Array
Given an integer array nums of length n where all the integers of nums are in the range [1, n] and each integer appears once or twice, return an array of all the integers that appears twice.

You must write an algorithm that runs in O(n) time and uses only constant extra space.
```java
class Solution {
    public List<Integer> findDuplicates(int[] nums) {
        Set<Integer> s = new HashSet<>();
        List<Integer> res = new ArrayList<>();
        for(int i = 0; i < nums.length; i ++){
            if(!s.add(nums[i])){
                res.add(nums[i]);
            }
        }
        return res;
    }
}
```

### 48.Rotate Image
You are given an n x n 2D matrix representing an image, rotate the image by 90 degrees (clockwise).

You have to rotate the image in-place, which means you have to modify the input 2D matrix directly. DO NOT allocate another 2D matrix and do the rotation.
```java
class Solution {
    public void rotate(int[][] matrix) {
        for(int i = 0; i < matrix.length; i++){
            for(int j = i; j < matrix[0].length; j++){
                int tmp = matrix[i][j];
                matrix[i][j] = matrix[j][i];
                matrix[j][i] = tmp;
            }
        }
        
        for(int i = 0; i < matrix.length; i++){
            for(int j = 0; j < matrix.length/2; j++){
                int temp = matrix[i][j];
                matrix[i][j] = matrix[i][matrix.length - j - 1];
                matrix[i][matrix.length - j - 1] = temp;
            }
        }
    }
}
```

### 75.Sort Colors
Given an array nums with n objects colored red, white, or blue, sort them in-place so that objects of the same color are adjacent, with the colors in the order red, white, and blue.

We will use the integers 0, 1, and 2 to represent the color red, white, and blue, respectively.

You must solve this problem without using the library's sort function.
```java
class Solution {
    public void sortColors(int[] nums) {
        int c0 = 0, c1 = 0, c2 = 0;
        for(int i = 0; i < nums.length; i++){
            if(nums[i] == 0) c0++;
            else if(nums[i] == 1) c1++;
            else c2++;
        }
        
        for(int j = 0; j < nums.length; j++){
            if(j < c0) nums[j] = 0;
            else if(j < c0 + c1) nums[j] = 1;
            else nums[j] = 2;
        }
    }
}
```

### 57.Insert Interval
You are given an array of non-overlapping intervals intervals where intervals[i] = [starti, endi] represent the start and the end of the ith interval and intervals is sorted in ascending order by starti. You are also given an interval newInterval = [start, end] that represents the start and end of another interval.

Insert newInterval into intervals such that intervals is still sorted in ascending order by starti and intervals still does not have any overlapping intervals (merge overlapping intervals if necessary).

Return intervals after the insertion.
```java
class Solution {
    public int[][] insert(int[][] intervals, int[] newInterval) {
        List<int []> res = new ArrayList<>();
        
        for(int[] slot : intervals){
            if(newInterval[1] < slot[0]){
                res.add(newInterval);
                newInterval = slot;
            }
            else if(slot[1] < newInterval[0]){
                res.add(slot);
            }else{
                newInterval[0] = Math.min(newInterval[0], slot[0]);
                newInterval[1] = Math.max(newInterval[1], slot[1]);
            }
        }
        res.add(newInterval);
        
        return res.toArray(new int[res.size()][]);
    }
}
```