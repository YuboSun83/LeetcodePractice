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
443.String Compression
151.Reverse Words in a String
809.Expressive Words
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

### 824.Goat Latin
You are given a string sentence that consist of words separated by spaces. Each word consists of lowercase and uppercase letters only.

We would like to convert the sentence to "Goat Latin" (a made-up language similar to Pig Latin.) The rules of Goat Latin are as follows:

If a word begins with a vowel ('a', 'e', 'i', 'o', or 'u'), append "ma" to the end of the word.
For example, the word "apple" becomes "applema".
If a word begins with a consonant (i.e., not a vowel), remove the first letter and append it to the end, then add "ma".
For example, the word "goat" becomes "oatgma".
Add one letter 'a' to the end of each word per its word index in the sentence, starting with 1.
For example, the first word gets "a" added to the end, the second word gets "aa" added to the end, and so on.
Return the final sentence representing the conversion from sentence to Goat Latin.
```java
class Solution {
    public String toGoatLatin(String sentence) {
        String[] s = sentence.split(" ");
        String trail = "maa";
        
        for(int i = 0; i < s.length; i++){
            if(!(Character.toLowerCase(s[i].charAt(0)) == 'a' || Character.toLowerCase(s[i].charAt(0)) == 'e' || Character.toLowerCase(s[i].charAt(0)) == 'i' || Character.toLowerCase(s[i].charAt(0)) == 'o' || Character.toLowerCase(s[i].charAt(0)) == 'u')){
                            s[i] = s[i].substring(1, s[i].length()) + s[i].charAt(0);
            }

            s[i] += trail;
            trail += "a";
            if(i != s.length - 1){
                s[i] += " ";
            }
        }
        
        String res = "";
        for(int j = 0; j < s.length; j++){
            res += s[j];
        }
        
        return res;
    }
}
```

### 415.Add Strings
Given two non-negative integers, num1 and num2 represented as string, return the sum of num1 and num2 as a string.

You must solve the problem without using any built-in library for handling large integers (such as BigInteger). You must also not convert the inputs to integers directly.
```java
class Solution {
    public String addStrings(String num1, String num2) {
        int i = num1.length() - 1;
        int j = num2.length() - 1;
        int carry = 0;
        
        StringBuilder sb = new StringBuilder();
        
        while(i >= 0 || j >= 0 || carry > 0){
            int n1 = 0;
            int n2 = 0;
            if(i >= 0){
                n1 = num1.charAt(i) - '0';
                i--;
            }
            if(j >= 0){
                n2 = num2.charAt(j) - '0';
                j--;
            }
            int num = (n1 + n2 + carry) % 10;
            carry = (n1 + n2 + carry) >= 10 ? 1 : 0;
            sb.append(num);
        }
        return sb.reverse().toString();
    }
}
```

### 14.Longest Common Prefix
Write a function to find the longest common prefix string amongst an array of strings.

If there is no common prefix, return an empty string "".
```java
class Solution {
    public String longestCommonPrefix(String[] strs) {
        String prefix = strs[0];
        for(int i = 0; i < strs.length; i++){
            while(strs[i].indexOf(prefix) != 0){
                prefix = prefix.substring(0, prefix.length() - 1);
            }
        }
        return prefix;
    }
}
```

### 28.Implement strStr()
Implement strStr().

Given two strings needle and haystack, return the index of the first occurrence of needle in haystack, or -1 if needle is not part of haystack.

Clarification:

What should we return when needle is an empty string? This is a great question to ask during an interview.

For the purpose of this problem, we will return 0 when needle is an empty string. This is consistent to C's strstr() and Java's indexOf().
```java
class Solution {
    public int strStr(String haystack, String needle) {
        int l1 = haystack.length();
        int l2 = needle.length();
        
        if(l2 > l1) return -1;
        if(l2 == 0) return 0;
        
        for(int i = 0; i <= l1 - l2; i++){
            if(haystack.substring(i, i + l2).equals(needle)) return i;
        }
        return -1;
    }
}
```

### 557.Reverse Words in a String III
Given a string s, reverse the order of characters in each word within a sentence while still preserving whitespace and initial word order.
```java
class Solution {
    public String reverseWords(String s) {
        String[] sq = s.split(" ");
        StringBuilder res = new StringBuilder();
        for(int i = 0; i < sq.length; i++){
            StringBuilder sb = new StringBuilder(sq[i]);
            res.append(sb.reverse().toString());
            if(i != sq.length - 1) res.append(" ");
        }
        return res.toString();
    }
}
```

### 6.ZigZag Conversion
The string "PAYPALISHIRING" is written in a zigzag pattern on a given number of rows like this: (you may want to display this pattern in a fixed font for better legibility)

P   A   H   N
A P L S I I G
Y   I   R
And then read line by line: "PAHNAPLSIIGYIR"
```java
class Solution {
    public String convert(String s, int numRows) {
        if(numRows == 1) return s;
        List<StringBuilder> rows = new ArrayList<>();
        
        for(int i = 0; i < Math.min(s.length(), numRows); i++){
            rows.add(new StringBuilder());
        }
        
        int curRow = 0;
        boolean goingDown = false;
        
        for(char c : s.toCharArray()){
            rows.get(curRow).append(c);
            if(curRow == 0 || curRow == numRows - 1) goingDown = !goingDown;
            curRow += goingDown? 1 : -1;
        }
        
        StringBuilder sb = new StringBuilder();
        for(StringBuilder row : rows) sb.append(row);
        return sb.toString();
    }
}
```

### 443.String Compression
Given an array of characters chars, compress it using the following algorithm:

Begin with an empty string s. For each group of consecutive repeating characters in chars:

If the group's length is 1, append the character to s.
Otherwise, append the character followed by the group's length.
The compressed string s should not be returned separately, but instead, be stored in the input character array chars. Note that group lengths that are 10 or longer will be split into multiple characters in chars.

After you are done modifying the input array, return the new length of the array.

You must write an algorithm that uses only constant extra space.

```java
class Solution {
    public int compress(char[] chars) {
        char pc = chars[0];
        StringBuilder sb = new StringBuilder();
        int count = 1;
        sb.append(pc);
        
        for(int i = 1; i < chars.length; i++){
            char cc = chars[i];
            if(pc == cc) count ++;
            else{
                pc = cc;
                if(count != 1) sb.append(count);
                count = 1;
                sb.append(pc);
            }
        }
        if(count != 1) sb.append(count);
        
        for(int j = 0; j < sb.length(); j++){
            chars[j] = sb.charAt(j);
        }
        return sb.length();
    }
}
```

### 848.Shifting Letters
You are given a string s of lowercase English letters and an integer array shifts of the same length.

Call the shift() of a letter, the next letter in the alphabet, (wrapping around so that 'z' becomes 'a').

For example, shift('a') = 'b', shift('t') = 'u', and shift('z') = 'a'.
Now for each shifts[i] = x, we want to shift the first i + 1 letters of s, x times.

Return the final string after all such shifts to s are applied.
```java
class Solution {
    public String shiftingLetters(String s, int[] shifts) {
        StringBuilder sb = new StringBuilder();
        int x = 0;
        for(int shift : shifts){
            x = (x + shift) % 26;
        }
        
        for(int i = 0; i < s.length(); i++){
            int index = s.charAt(i) - 'a';
            sb.append((char)((index + x) % 26 + 97));
            x = Math.floorMod(x - shifts[i], 26);
        }
        
        return sb.toString();
    }
}
```
