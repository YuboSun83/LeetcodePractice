### EASY
551.Student Attendance Record I
344.Reverse String
937.Reorder Data in Log Files
824.Goat Latin
415.Add Strings
14.Longest Common Prefix
28.Implement strStr()
557.Reverse Words in a String III

### MEDIUM
6.ZigZag Conversion
8.String to Integer (atoi
443.String Compression
151.Reverse Words in a String
186.Reverse Words in a String II
809.Expressive Words
616.Add Bold Tag in String
848.Shifting Letters

### HARD
68.Text Justification
1328*.Break a Palindrome

### 551.Student Attendance Record I
You are given a string s representing an attendance record for a student where each character signifies whether the student was absent, late, or present on that day. The record only contains the following three characters:

'A': Absent.
'L': Late.
'P': Present.
The student is eligible for an attendance award if they meet both of the following criteria:

The student was absent ('A') for strictly fewer than 2 days total.
The student was never late ('L') for 3 or more consecutive days.
Return true if the student is eligible for an attendance award, or false otherwise.

```java
class Solution {
    public boolean checkRecord(String s) {
        int a = 0, l = 0;
        for(int i = 0; i < s.length(); i++){
            if(s.charAt(i) == 'A'){
                a++;
                if(a == 2) return false;
            }
            
            if(s.charAt(i) == 'L') l++;
            if(s.charAt(i) == 'A' || s.charAt(i) == 'P') l = 0;
            if(l == 3) return false;
        }
        return true;
    }
}
```

### 344.Reverse String
Write a function that reverses a string. The input string is given as an array of characters s.

You must do this by modifying the input array in-place with O(1) extra memory.

```java
class Solution {
    public void reverseString(char[] s) {
        if(s.length < 2) return;
        int i = 0, j = s.length - 1;
        while(i < j){
            swap(s, i++, j--);
        }
    }
    private void swap(char[] s, int i, int j){
        char a = s[j];
        s[j] = s[i];
        s[i] = a;
    }
}
```

### 937.Reorder Data in Log Files
You are given an array of logs. Each log is a space-delimited string of words, where the first word is the identifier.

There are two types of logs:

Letter-logs: All words (except the identifier) consist of lowercase English letters.
Digit-logs: All words (except the identifier) consist of digits.
Reorder these logs so that:

The letter-logs come before all digit-logs.
The letter-logs are sorted lexicographically by their contents. If their contents are the same, then sort them lexicographically by their identifiers.
The digit-logs maintain their relative ordering.
Return the final order of the logs.
```java
class Solution {
    public String[] reorderLogFiles(String[] logs) {
        List<String> alpha = new ArrayList<>();
        List<String> nums = new ArrayList<>();
        
        for(int i = 0; i < logs.length; i++){
            String cur = logs[i];
            int pos = cur.indexOf(" ");
            char ch = cur.charAt(pos + 1);
            if(ch >= '0' && ch <= '9') nums.add(cur);
            else alpha.add(cur);
        }
        
        alpha.sort(new Comparator<String>(){
            @Override
            public int compare(String o1, String o2){
                int pos1 = o1.indexOf(" ");
                int pos2 = o2.indexOf(" ");
                
                String str1 = o1.substring(pos1 + 1);
                String str2 = o2.substring(pos2 + 1);
                
                int cmp = str1.compareTo(str2);
                if(cmp == 0){
                    return o1.substring(0, pos1).compareTo(o2.substring(0, pos2));
                }else{
                    return cmp;
                }
            }
        });
        
        String[] res = new String[logs.length];
        int index = 0;
        for(int i = 0; i < logs.length; i++){
            if(i < alpha.size()){
                res[index++] = alpha.get(i);
            }else{
                res[index++] = nums.get(i - alpha.size());
            }
        }
        
        return res;
    }
}
```