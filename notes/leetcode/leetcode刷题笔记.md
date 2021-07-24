[TOC]



# 刷题顺序和题目推荐

**一. 数组**

题目分类	题目编号
数组的遍历	485、495、414、628
统计数组中的元素	645、697、448、442、41、274
数组的改变、移动	453、665、283
二维数组及滚动数组	118、119、661、598、419
数组的旋转	189、396
特定顺序遍历二维数组	54、59、498
二维数组变换	566、48、73、289
前缀和数组	303、304、238
题解	数组篇

## **二. 字符串**

| **题目分类**           | **题目编号**                                                 |
| :--------------------- | ------------------------------------------------------------ |
| **字符**               | **520**                                                      |
| **回文串的定义**       | **125**                                                      |
| **公共前缀**           | **14**                                                       |
| **单词**               | **434、58**                                                  |
| **字符串的反转**       | **344、541、557、151**                                       |
| **字符的统计**         | **387、389、383、242、49、451、423、657、551、696、467、535** |
| **数字与字符串间转换** | **299、412、506、539、553、537、592、640、38、443、8、13、12、273、165、481** |
| **子序列**             | **392、524、521、522**                                       |
| **高精度运算**         | **66、67、415、43、306**                                     |
| **字符串变换**         | **482、6、68**                                               |
| **字符串匹配**         | **28、686、459、214**                                        |
| **中心拓展法**         | **5、647**                                                   |

### **回文串的定义**

### [125. 验证回文串](https://leetcode-cn.com/problems/valid-palindrome/)

给定一个字符串，验证它是否是回文串，只考虑字母和数字字符，可以忽略字母的大小写。

**说明：**本题中，我们将空字符串定义为有效的回文串。

**示例 1:**

```
输入: "A man, a plan, a canal: Panama"
输出: true
```

**示例 2:**

```
输入: "race a car"
输出: false
```

```java
class Solution {
    public boolean isPalindrome(String s) {
        int l = s.length();
        int i =0;
        int j = l-1;
        while(i<j){
            while(i<j&&Character.isLetterOrDigit(s.charAt(i))==false)i++;
            while(i<j&&Character.isLetterOrDigit(s.charAt(j))==false)j--;
            char c1 = Character.toLowerCase(s.charAt(i));
            char c2 = Character.toLowerCase(s.charAt(j));
            if(c1!=c2)return false;
            i++;
            j--;
        }
        return true;
    }
}
```

### [14. 最长公共前缀](https://leetcode-cn.com/problems/longest-common-prefix/)

编写一个函数来查找字符串数组中的最长公共前缀。

如果不存在公共前缀，返回空字符串 `""`。

**示例 1：**

```
输入：strs = ["flower","flow","flight"]
输出："fl"
```

**示例 2：**

```
输入：strs = ["dog","racecar","car"]
输出：""
解释：输入不存在公共前缀。
```

**提示：**

- `0 <= strs.length <= 200`
- `0 <= strs[i].length <= 200`
- `strs[i]` 仅由小写英文字母组成

```java
//方法一 中规中矩把 复习一下字符串的常用操作  横向扫描
class Solution {
    public String longestCommonPrefix(String[] strs) {
        if(strs.length==0)return "";
        int length = strs.length;
        String prefix = strs[0];
        for(int i=1;i<length;i++){
            prefix = longestCommonPrefix(prefix,strs[i]);
            if(prefix=="")break;
        }
        return prefix;   
    }
    public String longestCommonPrefix(String str1,String str2){
        int length = Math.min(str1.length(),str2.length());
        int index=0;
        while(index<length){
            if(str1.charAt(index)!=str2.charAt(index)){
                break;
            }
            index++;
        }
        return str1.substring(0,index);
    }
}
//方法二 纵向扫描  比较简单 直接抄答案了
class Solution {
    public String longestCommonPrefix(String[] strs) {
        if (strs == null || strs.length == 0) {
            return "";
        }
        int length = strs[0].length();
        int count = strs.length;
        for (int i = 0; i < length; i++) {
            char c = strs[0].charAt(i);
            for (int j = 1; j < count; j++) {
                if (i == strs[j].length() || strs[j].charAt(i) != c) {
                    return strs[0].substring(0, i);
                }
            }
        }
        return strs[0];
    }
}
```

### [434. 字符串中的单词数](https://leetcode-cn.com/problems/number-of-segments-in-a-string/)

统计字符串中的单词个数，这里的单词指的是连续的不是空格的字符。

请注意，你可以假定字符串里不包括任何不可打印的字符。

**示例:**

```
输入: "Hello, my name is John"
输出: 5
解释: 这里的单词是指连续的不是空格的字符，所以 "Hello," 算作 1 个单词。
```

```java
class Solution {
    public int countSegments(String s) {
       int count = 0;
       int l = s.length();
       for(int i=0;i<l;i++){
           if((i==0||(s.charAt(i-1)==' '))&&s.charAt(i)!=' ')count++;
       }
       return count;
    }
}
```

### [58. 最后一个单词的长度](https://leetcode-cn.com/problems/length-of-last-word/)

给你一个字符串 `s`，由若干单词组成，单词之间用空格隔开。返回字符串中最后一个单词的长度。如果不存在最后一个单词，请返回 0 。

**单词** 是指仅由字母组成、不包含任何空格字符的最大子字符串。

 

**示例 1：**

```
输入：s = "Hello World"
输出：5
```

**示例 2：**

```
输入：s = " "
输出：0
```

**提示：**

- `1 <= s.length <= 104`
- `s` 仅有英文字母和空格 `' '` 组成

```java
class Solution {
    public int lengthOfLastWord(String s) {
        if(s.length()==0)return 0;
        String []str = s.split(" ");
        int l = str.length;
        if(l==0) return 0;
        return str[l-1].length();
    }
}
class Solution {
    public int lengthOfLastWord(String s) {
        if(s.length()==0)return 0;
        int count = 0;
        int index = s.length()-1;
        while(s.charAt(index)==' '&&index>0){
            index--;
        }
        for(int i = index;i>=0;i--){
            if(s.charAt(i)==' ')break;
            count++;
        }
        return count;
    }
}
```

### [344. 反转字符串](https://leetcode-cn.com/problems/reverse-string/)

编写一个函数，其作用是将输入的字符串反转过来。输入字符串以字符数组 `char[]` 的形式给出。

不要给另外的数组分配额外的空间，你必须**[原地](https://baike.baidu.com/item/原地算法)修改输入数组**、使用 O(1) 的额外空间解决这一问题。

你可以假设数组中的所有字符都是 [ASCII](https://baike.baidu.com/item/ASCII) 码表中的可打印字符。

 

**示例 1：**

```
输入：["h","e","l","l","o"]
输出：["o","l","l","e","h"]
```

**示例 2：**

```
输入：["H","a","n","n","a","h"]
输出：["h","a","n","n","a","H"]
```

```java
class Solution {
    public void reverseString(char[] s) {
        int length = s.length;
        if(length!=0){
            int first = 0;
            int last = length-1;
            while(true){
                if(first>=last)break;
                char tmp = s[first];
                s[first] = s[last];
                s[last] = tmp;
                first++;
                last--;
            }
        }
    }
}
```

### [541. 反转字符串 II](https://leetcode-cn.com/problems/reverse-string-ii/)

给定一个字符串 `s` 和一个整数 `k`，你需要对从字符串开头算起的每隔 `2k` 个字符的前 `k` 个字符进行反转。

- 如果剩余字符少于 `k` 个，则将剩余字符全部反转。
- 如果剩余字符小于 `2k` 但大于或等于 `k` 个，则反转前 `k` 个字符，其余字符保持原样。

**示例:**

```
输入: s = "abcdefg", k = 2
输出: "bacdfeg"
```

 

**提示：**

1. 该字符串只包含小写英文字母。
2. 给定字符串的长度和 `k` 在 `[1, 10000]` 范围内。

```java
//自己写的麻烦方法
class Solution {
    public String reverseStr(String s, int k) {
        int length = s.length();
        int x = length/(2*k);
        int y = length%(2*k);
        StringBuilder res = new StringBuilder();
        int index = 0;
        for(int i =0;i<x;i++){
            StringBuilder tmp = new StringBuilder();
            tmp.append(s.substring(index,index+k));
            index = index+k;
            tmp = tmp.reverse();
            tmp.append(s.substring(index,index+k));
            res.append(tmp.toString());
            index = index+k;
        }
        if(y<k){
            StringBuilder tmp  = new StringBuilder(s.substring(index,index+y));
            tmp = tmp.reverse();
            res.append(tmp.toString());
        }else if(y>=k&&y<2*k){
            StringBuilder tmp  = new StringBuilder(s.substring(index,index+k)); 
            tmp = tmp.reverse();
            index = index+k;
            tmp.append(s.substring(index,length));
            res.append(tmp.toString());
        }
        return res.toString();
    }
}

//官方的简单方法
class Solution {
    public String reverseStr(String s, int k) {
        int length = s.length();
        char[]str = s.toCharArray();
        for(int start = 0;start<length;start+=2*k){
            int i = start;
            int j = Math.min(start+k-1,length-1);//亮点
                while(i<j){
                    char tmp = str[i];
                    str[i++] = str[j];
                    str[j--] = tmp;
                }
            }
        return new String(str);//char2String
        }
}
```



### [557. 反转字符串中的单词 III](https://leetcode-cn.com/problems/reverse-words-in-a-string-iii/)

给定一个字符串，你需要反转字符串中每个单词的字符顺序，同时仍保留空格和单词的初始顺序。

**示例：**

```
输入："Let's take LeetCode contest"
输出："s'teL ekat edoCteeL tsetnoc"
```

 

***\**\*\*\*提示：\*\*\*\*\****

- 在字符串中，每个单词由单个空格分隔，并且字符串中不会有任何额外的空格。

```java
class Solution {
    public String reverseWords(String s) {
        if(s.length()==0)return "";
        String[]strs = s.split(" ");
        StringBuilder res = new StringBuilder();
        for(int i =0;i<strs.length;i++){
            StringBuilder sb = new StringBuilder(strs[i]);
            sb = sb.reverse();
            res.append(sb);
            if(i!=strs.length-1)res.append(" ");
        }
        return res.toString();
    }
}
```

### [151. 翻转字符串里的单词](https://leetcode-cn.com/problems/reverse-words-in-a-string/)

给定一个字符串，逐个翻转字符串中的每个单词。

**说明：**

- 无空格字符构成一个 **单词** 。
- 输入字符串可以在前面或者后面包含多余的空格，但是反转后的字符不能包括。
- 如果两个单词间有多余的空格，将反转后单词间的空格减少到只含一个。

 

**示例 1：**

```
输入："the sky is blue"
输出："blue is sky the"
```

**示例 2：**

```
输入："  hello world!  "
输出："world! hello"
解释：输入字符串可以在前面或者后面包含多余的空格，但是反转后的字符不能包括。
```

**示例 3：**

```
输入："a good   example"
输出："example good a"
解释：如果两个单词间有多余的空格，将反转后单词间的空格减少到只含一个。
```

**示例 4：**

```
输入：s = "  Bob    Loves  Alice   "
输出："Alice Loves Bob"
```

**示例 5：**

```
输入：s = "Alice does not even like bob"
输出："bob like even not does Alice"
```

**提示：**

- `1 <= s.length <= 104`
- `s` 包含英文大小写字母、数字和空格 `' '`
- `s` 中 **至少存在一个** 单词

```java
class Solution {
    public String reverseWords(String s) {
        s=s.trim();//去掉首位空格符
        String []strs = s.split("\\s+");//正则表达式，若有多个空格也一并去除
        StringBuilder res = new StringBuilder();
        for(int i =strs.length-1;i>=0;i--){
            res.append(strs[i]);
            if(i!=0){
               res.append(" ");
            }
        }
        return res.toString();
    }
}
//答案的解法
class Solution {
    public String reverseWords(String s) {
        s=s.trim();
        List<String>wordList = Arrays.asList(s.split("\\s+"));//
        Collections.reverse(wordList);//
        return String.join(" ",wordList);//这几种方法都没用过，可以记下来
    }
}
```

### [387. 字符串中的第一个唯一字符](https://leetcode-cn.com/problems/first-unique-character-in-a-string/)

给定一个字符串，找到它的第一个不重复的字符，并返回它的索引。如果不存在，则返回 -1。

**示例：**

```
s = "leetcode"
返回 0

s = "loveleetcode"
返回 2
```

 

**提示：**你可以假定该字符串只包含小写字母。

```java
//哈希表 HashMap遍历两次   value存储的是char的次数
class Solution {
    public int firstUniqChar(String s) {
        Map<Character,Integer> map = new HashMap<>();
        for(int i=0;i<s.length();i++){
            char c = s.charAt(i);
            map.put(c,map.getOrDefault(c,0)+1);
        }
        for(int i =0;i<s.length();i++){
            char c = s.charAt(i);
            if(map.get(c)==1) return i;
        }
        return -1;
    }
}
//同样两次遍历HashMap， 存储的value不同 为索引
class Solution {
    public int firstUniqChar(String s) {
        Map<Character,Integer> map = new HashMap<>();
        for(int i=0;i<s.length();i++){
            char c = s.charAt(i);
            if(map.containsKey(c)){
                map.put(c,-1);
            }else{
                map.put(c,i);
            }
        }
        for(int i =0;i<s.length();i++){
            char c = s.charAt(i);
            if(map.get(c)!=-1) return i;
        }
        return -1;
    }
}
```

### [389. 找不同](https://leetcode-cn.com/problems/find-the-difference/)

给定两个字符串 ***s*** 和 ***t***，它们只包含小写字母。

字符串 ***t\*** 由字符串 ***s\*** 随机重排，然后在随机位置添加一个字母。

请找出在 ***t*** 中被添加的字母。

```java
//遍历三遍HashMap 自己的解法 很慢
class Solution {
    public char findTheDifference(String s, String t) {
        Map<Character,Integer>map1 = new HashMap<>();
        Map<Character,Integer>map2 = new HashMap<>();
        for(int i =0;i<s.length();i++){
            char c = s.charAt(i);
            map1.put(c,map1.getOrDefault(c,0)+1);
        }
        for(int i =0;i<t.length();i++){
            char c = t.charAt(i);
            map2.put(c,map2.getOrDefault(c,0)+1);
        }
        for(int i =0;i<t.length();i++){
            char c = t.charAt(i);
            if(map1.get(c)==null||map1.get(c)!=map2.get(c))return c;
        }
        return ' ';
    }
}
//自己写的遍历两边HashMap 还是很慢
class Solution {
    public char findTheDifference(String s, String t) {
        Map<Character,Integer>map = new HashMap<>();
        for(int i =0;i<s.length();i++){
            char c = s.charAt(i);
            map.put(c,map.getOrDefault(c,0)+1);
        }
        for(int i =0;i<t.length();i++){
            char c = t.charAt(i);
            if(map.get(c)==null||map.get(c)==0)return c;
            map.put(c,map.get(c)-1);
        }
        return ' ';
    }
}
//用不到HashMap 只用一个数组就可以 和方法2思想一样
class Solution {
    public char findTheDifference(String s, String t) {
        int []chars = new int [26];
        for(int i =0;i<s.length();i++){
            char c = s.charAt(i);
            chars[c-'a']++;
        }
        for(int i =0;i<t.length();i++){
            char c = t.charAt(i);
            chars[c-'a']--;
            if(chars[c-'a']==-1){
                return c;
            }
        }
        return ' ';
    }
}
// 思路不错的解法
class Solution {
    public char findTheDifference(String s, String t) {
        int res = 0;
        for(int i =0;i<t.length();i++){
            res+=t.charAt(i);
        }
        for(int i =0;i<s.length();i++){
            res-=s.charAt(i);
        }
        return (char)res;
    }
}
//位运算 异或运算  a⊕a = 0     a⊕0 = a
class Solution {
    public char findTheDifference(String s, String t) {
        int res = 0;
        String str = s+t;
        for(int i=0;i<str.length();i++){
            res^=str.charAt(i);
        }
        return (char)res;
    }
}
```

### [383. 赎金信](https://leetcode-cn.com/problems/ransom-note/)

给定一个赎金信 (`ransom`) 字符串和一个杂志(`magazine`)字符串，判断第一个字符串 `ransom` 能不能由第二个字符串 `magazines` 里面的字符构成。如果可以构成，返回 `true` ；否则返回 `false`。

(题目说明：为了不暴露赎金信字迹，要从杂志上搜索各个需要的字母，组成单词来表达意思。杂志字符串中的每个字符只能在赎金信字符串中使用一次。)

**注意：**

你可以假设两个字符串均只含有小写字母。

```
canConstruct("a", "b") -> false
canConstruct("aa", "ab") -> false
canConstruct("aa", "aab") -> true
```

```java
//和上个题基本一样
class Solution {
    public boolean canConstruct(String ransomNote, String magazine) {
        Map<Character,Integer> map = new HashMap<>();
        for(int i=0;i<magazine.length();i++){
            char c = magazine.charAt(i);
            map.put(c,map.getOrDefault(c,0)+1);
        }
        for(int i =0;i<ransomNote.length();i++){
            char c = ransomNote.charAt(i);
            if(map.get(c)==null||map.get(c)==0)return false;
            map.put(c,map.get(c)-1);
        }
        return true;
    }
}
```



**三. 数与位**

题目分类	题目编号
数字的位操作	7、9、479、564、231、342、326、504、263、190、191、476、461、477、693、393、172、458、258、319、405、171、168、670、233、357、400
简单数学题	492、29、507
快速幂	50、372

**四. 栈与递归**

题目分类	题目编号
用栈访问最后若干元素	682、71、388
栈与计算器	150、227、224
栈与括号匹配	20、636、591、32
递归	385、341、394

**五. 链表**

题目分类	题目编号
链表的删除	203、237、19
链表的遍历	430
链表的旋转与反转	61、24、206、92、25
链表高精度加法	2、445
链表的合并	21、23

**六. 哈希表**

题目分类	题目编号
哈希表的查找、插入及删除	217、633、349、128、202、500、290、532、205、166、466、138
哈希表与索引	1、167、599、219、220
哈希表与统计	594、350、554、609、454、18
哈希表与前缀和	560、523、525

**七. 贪心算法**

题目分类	题目编号
数组与贪心算法	605、121、122、561、455、575、135、409、621、179、56、57、228、452、435、646、406、48、169、215、75、324、517、649、678、420
子数组与贪心算法	53、134、581、152
子序列与贪心算法	334、376、659
数字与贪心	343
单调栈法	496、503、456、316、402、321、84、85

## **八. 双指针法**

| **题目分类**             | **题目编号**                                                 |
| ------------------------ | ------------------------------------------------------------ |
| **头尾指针**             | **345、680、167、15、16、18、11、42**                        |
| **同向双指针、滑动窗口** | **27、26、80、83、82、611、187、643、674、209、3、438、567、424、76、30** |
| **分段双指针**           | **86、328、160、88、475**                                    |
| **快慢指针**             | **141、142、143、234、457、287**                             |



### **同向双指针、滑动窗口**

#### [3. 无重复字符的最长子串](https://leetcode-cn.com/problems/longest-substring-without-repeating-characters/)

给定一个字符串，请你找出其中不含有重复字符的 **最长子串** 的长度。

**示例 1:**

```
输入: s = "abcabcbb"
输出: 3 
解释: 因为无重复字符的最长子串是 "abc"，所以其长度为 3。
```

**示例 2:**

```
输入: s = "bbbbb"
输出: 1
解释: 因为无重复字符的最长子串是 "b"，所以其长度为 1。
```

**示例 3:**

```
输入: s = "pwwkew"
输出: 3
解释: 因为无重复字符的最长子串是 "wke"，所以其长度为 3。
     请注意，你的答案必须是 子串 的长度，"pwke" 是一个子序列，不是子串。
```

**示例 4:**

```
输入: s = ""
输出: 0
```

**提示：**

- `0 <= s.length <= 5 * 104`
- `s` 由英文字母、数字、符号和空格组成

```JAVA
//////此题属于算法小抄中滑动窗口的第三题，套用模板既可以解题
class Solution {
    public int lengthOfLongestSubstring(String s) {
        int res = 0;
        Map<Character,Integer>window = new HashMap<>();
        int left=0,right=0;
        int sLength = s.length();
        while(right<sLength){
            char c = s.charAt(right);
            window.put(c,window.getOrDefault(c,0)+1);
            right++;
            while(window.get(c)>1){
                char tmp = s.charAt(left);
                left++;
                window.put(tmp,window.get(tmp)-1);
            }
            res = Math.max(res,right-left);
        }
        return res;
    }
}
//自己的解法
class Solution {
    public int lengthOfLongestSubstring(String s) {
        int res = 0;
        Map<Character,Integer>window = new HashMap<>();
        int left=0,right=0;
        int sLength = s.length();
        while(right<sLength){
            char c = s.charAt(right);
            if(window.containsKey(c)){
                left = Math.max(left,window.get(c)+1);
                window.put(c,right);
            }else{
                window.put(c,right);
            }
            res = Math.max(res,right-left+1);
            right++;
           
        }
        return sLength==1? 1:res;
    }
}
```



#### [438. 找到字符串中所有字母异位词](https://leetcode-cn.com/problems/find-all-anagrams-in-a-string/)

给定一个字符串 **s** 和一个非空字符串 **p**，找到 **s** 中所有是 **p** 的字母异位词的子串，返回这些子串的起始索引。

字符串只包含小写英文字母，并且字符串 **s** 和 **p** 的长度都不超过 20100。

**说明：**

- 字母异位词指字母相同，但排列不同的字符串。
- 不考虑答案输出的顺序。

**示例 1:**

```
输入:
s: "cbaebabacd" p: "abc"

输出:
[0, 6]

解释:
起始索引等于 0 的子串是 "cba", 它是 "abc" 的字母异位词。
起始索引等于 6 的子串是 "bac", 它是 "abc" 的字母异位词。
```

 **示例 2:**

```
输入:
s: "abab" p: "ab"

输出:
[0, 1, 2]

解释:
起始索引等于 0 的子串是 "ab", 它是 "ab" 的字母异位词。
起始索引等于 1 的子串是 "ba", 它是 "ab" 的字母异位词。
起始索引等于 2 的子串是 "ab", 它是 "ab" 的字母异位词。
```

```JAVA
////此题属于算法小抄中滑动窗口的第三题，套用模板既可以解题
class Solution {
    public List<Integer> findAnagrams(String s, String p) {
        List<Integer>res = new ArrayList<>();
        Map<Character,Integer>need = new HashMap<>();
        Map<Character,Integer>window = new HashMap<>();
        int left=0,right=0;
        int valid=0;
        int sLength = s.length(),pLength = p.length();
        for(int i =0;i<pLength;i++){
            char c = p.charAt(i);
            need.put(c,need.getOrDefault(c,0)+1);
        }
        while(right<sLength){
            char c = s.charAt(right);
            right++;
            if(need.containsKey(c)){
                window.put(c,window.getOrDefault(c,0)+1);
                if(window.get(c).equals(need.get(c))) valid++;
            }

            while(right-left>=pLength){
                char leftc = s.charAt(left);
                if(valid==need.size()) res.add(left);
                left++;
                if(need.containsKey(leftc)){
                    if(need.get(leftc).equals(window.get(leftc)))valid--;
                    window.put(leftc,window.get(leftc)-1);
                }
            }
        }
        return res;
    }
}
```



#### [567. 字符串的排列](https://leetcode-cn.com/problems/permutation-in-string/)

难度中等313

给定两个字符串 **s1** 和 **s2**，写一个函数来判断 **s2** 是否包含 **s1** 的排列。

换句话说，第一个字符串的排列之一是第二个字符串的子串。

 

**示例 1：**

```
输入: s1 = "ab" s2 = "eidbaooo"
输出: True
解释: s2 包含 s1 的排列之一 ("ba").
```

**示例 2：**

```
输入: s1= "ab" s2 = "eidboaoo"
输出: False
```

**提示：**

- 输入的字符串只包含小写字母
- 两个字符串的长度都在 [1, 10,000] 之间

```JAVA
////此题属于算法小抄中滑动窗口的第二题，套用模板既可以解题
class Solution {
    public boolean checkInclusion(String s1, String s2) {
        Map<Character,Integer>need = new HashMap<>();
        Map<Character,Integer>window = new HashMap<>();
        for(int i =0;i<s1.length();i++){
            char c = s1.charAt(i);
            need.put(c,need.getOrDefault(c,0)+1);
        }
        int left=0,right=0;
        int valid = 0;
        int s1Length = s1.length(),s2Length = s2.length();
        while(right<s2Length){
            char c = s2.charAt(right);
            right++;
            if(need.containsKey(c)){
                window.put(c,window.getOrDefault(c,0)+1);
                if(window.get(c).equals(need.get(c))){
                    valid++;
                }
            }
            while(right-left>=s1Length){
                if(valid==need.size())return true;
                char leftc = s2.charAt(left);
                if(need.containsKey(leftc)){
                    if(window.get(leftc).equals(need.get(leftc)))valid--;
                    window.put(leftc,window.get(leftc)-1);
                }
                left++;
            }
        }
        return false;
    }
}
```



#### [76. 最小覆盖子串](https://leetcode-cn.com/problems/minimum-window-substring/)

难度困难979

给你一个字符串 `s` 、一个字符串 `t` 。返回 `s` 中涵盖 `t` 所有字符的最小子串。如果 `s` 中不存在涵盖 `t` 所有字符的子串，则返回空字符串 `""` 。

**注意：**如果 `s` 中存在这样的子串，我们保证它是唯一的答案。

**示例 1：**

```
输入：s = "ADOBECODEBANC", t = "ABC"
输出："BANC"
```

**示例 2：**

```
输入：s = "a", t = "a"
输出："a"
```

**提示：**

- `1 <= s.length, t.length <= 105`
- `s` 和 `t` 由英文字母组成

**进阶：**你能设计一个在 `o(n)` 时间内解决此问题的算法吗？

```java
//此题属于算法小抄中滑动窗口的第一题，套用模板既可以解题
class Solution {
    public String minWindow(String s, String t) {
        Map<Character,Integer>need = new HashMap<>();
        Map<Character,Integer>window = new HashMap<>();
        for(int i =0;i<t.length();i++){
            char c = t.charAt(i);
            need.put(c,need.getOrDefault(c,0)+1);
        }
        int left=0,right=0;
        int start = 0,len = Integer.MAX_VALUE;
        int valid = 0;
        int s1Length = s.length(),s2Length = t.length();
        while(right<s1Length){
            char c = s.charAt(right);
            right++;
            if(need.containsKey(c)){
                window.put(c,window.getOrDefault(c,0)+1);
                if(window.get(c).equals(need.get(c))){
                    valid++;
                }
            }
            while(valid==need.size()){//左窗口收缩的表达式比较难找 是解决滑动窗口的核心问题
               if(right-left<len){
                   start = left;
                   len = right-left;
               }
                char leftc = s.charAt(left);
                if(need.containsKey(leftc)){
                    if(window.get(leftc).equals(need.get(leftc)))valid--;
                    window.put(leftc,window.get(leftc)-1);
                }
                left++;
            }
        }
        return len==Integer.MAX_VALUE? "":s.substring(start,start+len);
    }
}
```



## **九. 树**



| **题目分类**                 | **题目编号**                                                 |
| ---------------------------- | ------------------------------------------------------------ |
| **树与递归**                 | **100、222、101、226、437、563、617、508、572、543、654、687、87** |
| **树的层次遍历**             | **102、429、690、559、662、671、513、515、637、103、107、257、623、653、104、111、112、113、129、404、199、655、116、117** |
| **树的前序遍历**             | **144、589**                                                 |
| **树的前序序列化**           | **606、331、652、297、449**                                  |
| **树的后序遍历**             | **145、590**                                                 |
| **树的中序遍历与二叉搜索树** | **94、700、530、538、230、98、173、669、450、110、95、108、109** |
| **重构二叉树**               | **105、106**                                                 |
| **二叉树的展开**             | **114**                                                      |
| **最近公共祖先**             | **235、236**                                                 |
| **Morris中序遍历**           | **501、99**                                                  |
| **四叉树**                   | **558、427**                                                 |

## 树与递归

### [100. 相同的树](https://leetcode-cn.com/problems/same-tree/)

给你两棵二叉树的根节点 `p` 和 `q` ，编写一个函数来检验这两棵树是否相同。

如果两个树在结构上相同，并且节点具有相同的值，则认为它们是相同的。

 

**示例 1：**

![img](https://assets.leetcode.com/uploads/2020/12/20/ex1.jpg)

```
输入：p = [1,2,3], q = [1,2,3]
输出：true
```

**示例 2：**

![img](https://assets.leetcode.com/uploads/2020/12/20/ex2.jpg)

```
输入：p = [1,2], q = [1,null,2]
输出：false
```

**示例 3：**

![img](https://assets.leetcode.com/uploads/2020/12/20/ex3.jpg)

```
输入：p = [1,2,1], q = [1,1,2]
输出：false
```

 

**提示：**

- 两棵树上的节点数目都在范围 `[0, 100]` 内
- `-104 <= Node.val <= 104`

```java
//递归 简简单单
class Solution {
    public boolean isSameTree(TreeNode p, TreeNode q) {
        if(p==null&&q==null)return true;
        if(p==null||q==null||p.val!=q.val) return false;
        return isSameTree(p.left,q.left)&&isSameTree(p.right,q.right);
    }
}	
```

### [222. 完全二叉树的节点个数](https://leetcode-cn.com/problems/count-complete-tree-nodes/)

给你一棵 **完全二叉树** 的根节点 `root` ，求出该树的节点个数。

[完全二叉树](https://baike.baidu.com/item/完全二叉树/7773232?fr=aladdin) 的定义如下：在完全二叉树中，除了最底层节点可能没填满外，其余每层节点数都达到最大值，并且最下面一层的节点都集中在该层最左边的若干位置。若最底层为第 `h` 层，则该层包含 `1~ 2h` 个节点。

 

**示例 1：**

![img](https://assets.leetcode.com/uploads/2021/01/14/complete.jpg)

```
输入：root = [1,2,3,4,5,6]
输出：6
```

**示例 2：**

```
输入：root = []
输出：0
```

**示例 3：**

```
输入：root = [1]
输出：1
```

**提示：**

- 树中节点的数目范围是`[0, 5 * 104]`
- `0 <= Node.val <= 5 * 104`
- 题目数据保证输入的树是 **完全二叉树**

 

**进阶：**遍历树来统计节点是一种时间复杂度为 `O(n)` 的简单解决方案。你可以设计一个更快的算法吗？

```java
//递归 时间复杂度O(n) 常规解法
class Solution {
    public int countNodes(TreeNode root) {
        if(root==null)return 0;
        return 1+countNodes(root.left)+countNodes(root.right);
    }
}
//解法2 利用了完全二叉树的性质进行解题
class Solution {
    public int countNodes(TreeNode root) {
        if(root==null) return 0;
        int left = getDepth(root.left);
        int right = getDepth(root.right);
        if(left==right)return (countNodes(root.right)+(1<<left));//小技巧，使用移位运算计算2^left
        else return (countNodes(root.left)+(1<<right));//2^right
    }
    public int getDepth(TreeNode root){
        int depth = 0;
        while(root!=null){
            depth++;
            root = root.left;
        }
        return depth;
    }
}
```

### [101. 对称二叉树](https://leetcode-cn.com/problems/symmetric-tree/)

给定一个二叉树，检查它是否是镜像对称的。

例如，二叉树 `[1,2,2,3,4,4,3]` 是对称的。

```
    1
   / \
  2   2
 / \ / \
3  4 4  3 
```

但是下面这个 `[1,2,2,null,3,null,3]` 则不是镜像对称的:

```
    1
   / \
  2   2
   \   \
   3    3
```

**进阶：**

你可以运用递归和迭代两种方法解决这个问题吗？

```java
//递归解法
class Solution {
    public boolean isSymmetric(TreeNode root) {
        return root==null||isSymmetric(root.left,root.right);
    }
    public boolean isSymmetric(TreeNode left,TreeNode right){
        if(left==null&&right==null)return true;
        if(left==null||right==null||left.val!=right.val)return false;
        return isSymmetric(left.left,right.right)&&isSymmetric(left.right,right.left);
    }
}
//迭代解法
class Solution {
    public boolean isSymmetric(TreeNode root) {
        return check(root,root);
    }
    public boolean check(TreeNode left,TreeNode right){
        Queue<TreeNode>queue = new LinkedList<TreeNode>();
        queue.offer(left);
        queue.offer(right);
        while(!queue.isEmpty()){
            left = queue.poll();
            right = queue.poll();
            if(left==null&&right==null)continue;
            if(left==null||right==null||left.val!=right.val)return false;
            queue.offer(left.left);
            queue.offer(right.right);
            queue.offer(left.right);
            queue.offer(right.left);
        }
        return true;
    }
}
```

### [226. 翻转二叉树](https://leetcode-cn.com/problems/invert-binary-tree/)

翻转一棵二叉树。

**示例：**

输入：

```
     4
   /   \
  2     7
 / \   / \
1   3 6   9
```

输出：

```
     4
   /   \
  7     2
 / \   / \
9   6 3   1
```

**备注:**
这个问题是受到 [Max Howell ](https://twitter.com/mxcl)的 [原问题](https://twitter.com/mxcl/status/608682016205344768) 启发的 ：

> 谷歌：我们90％的工程师使用您编写的软件(Homebrew)，但是您却无法在面试时在白板上写出翻转二叉树这道题，这太糟糕了。



```java
//递归方法 没啥好说的
class Solution {
    public TreeNode invertTree(TreeNode root) {
        if(root==null)return null;
        TreeNode tmp = root.left;
        root.left = root.right;
        root.right = tmp;
        invertTree(root.left);
        invertTree(root.right);
        return root;
    }
}
//迭代方法，待补充
```

### [112. 路径总和](https://leetcode-cn.com/problems/path-sum/)

给你二叉树的根节点 `root` 和一个表示目标和的整数 `targetSum` ，判断该树中是否存在 **根节点到叶子节点** 的路径，这条路径上所有节点值相加等于目标和 `targetSum` 。

**叶子节点** 是指没有子节点的节点。

 

**示例 1：**

![img](https://assets.leetcode.com/uploads/2021/01/18/pathsum1.jpg)

```
输入：root = [5,4,8,11,null,13,4,7,2,null,null,null,1], targetSum = 22
输出：true
```

**示例 2：**

![img](https://assets.leetcode.com/uploads/2021/01/18/pathsum2.jpg)

```
输入：root = [1,2,3], targetSum = 5
输出：false
```

**示例 3：**

```
输入：root = [1,2], targetSum = 0
输出：false
```

 

**提示：**

- 树中节点的数目在范围 `[0, 5000]` 内
- `-1000 <= Node.val <= 1000`
- `-1000 <= targetSum <= 1000`

```java
class Solution {
    public boolean hasPathSum(TreeNode root, int targetSum) {
        if(root==null)return false;
        if(root.val==targetSum&&root.left==null&&root.right==null)return true;
        return hasPathSum(root.left,targetSum-root.val)||hasPathSum(root.right,targetSum-root.val);
    }
}
```

### [257. 二叉树的所有路径](https://leetcode-cn.com/problems/binary-tree-paths/)

给定一个二叉树，返回所有从根节点到叶子节点的路径。

**说明:** 叶子节点是指没有子节点的节点。

**示例:**

```
输入:

   1
 /   \
2     3
 \
  5

输出: ["1->2->5", "1->3"]

解释: 所有根节点到叶子节点的路径为: 1->2->5, 1->3
```

```java
class Solution {
    public List<String> binaryTreePaths(TreeNode root) {
        List<String> res = new ArrayList<String>();
        dfs(res,"",root);
        return res;
    }
    public void dfs(List<String>res,String path,TreeNode root){
        if(root!=null){
            StringBuilder sb = new StringBuilder(path);
            sb.append(Integer.toString(root.val));
            if(root.left==null&&root.right==null){
                path = sb.toString();
                res.add(path);
            }else{
                sb.append("->");
                path = sb.toString();
                dfs(res,path,root.left);
                dfs(res,path,root.right);
            }
        }
    }
}
```

### [113. 路径总和 II](https://leetcode-cn.com/problems/path-sum-ii/)

给定一个二叉树和一个目标和，找到所有从根节点到叶子节点路径总和等于给定目标和的路径。

**说明:** 叶子节点是指没有子节点的节点。

**示例:**
给定如下二叉树，以及目标和 `sum = 22`，

```
              5
             / \
            4   8
           /   / \
          11  13  4
         /  \    / \
        7    2  5   1
```

返回:

```
[
   [5,4,11,2],
   [5,8,4,5]
]
```

```java
//dfs 效率一般 核心在于使用subList来防止list被污染
class Solution {
    public List<List<Integer>> pathSum(TreeNode root, int targetSum) {
        List<List<Integer>> res = new ArrayList<List<Integer>>();
        List<Integer> cur = new ArrayList<Integer>();
        dfs(res,cur,root,targetSum);
        return res;
    }
    public void dfs(List<List<Integer>> res,List<Integer>cur,TreeNode root,int targetSum){
       if(root==null)return ;
       List<Integer> subList = new ArrayList<>(cur);
       subList.add(root.val);
       if(root.left==null&&root.right==null&&root.val==targetSum){
               res.add(subList);
       }else{
           dfs(res,subList,root.left,targetSum-root.val);
           dfs(res,subList,root.right,targetSum-root.val);
       }
    }
}
//回溯的方法 效率快不少 但存在一些疑问
class Solution {
    public List<List<Integer>> pathSum(TreeNode root, int targetSum) {
        List<List<Integer>> res = new ArrayList<List<Integer>>();
        List<Integer> cur = new ArrayList<Integer>();
        dfs(res,cur,root,targetSum);
        return res;
    }
    public void dfs(List<List<Integer>> res,List<Integer>cur,TreeNode root,int targetSum){
       if(root==null)return ;
       cur.add(root.val);
       if(root.left==null&&root.right==null&&root.val==targetSum){
               res.add(new ArrayList<Integer>(cur));
               cur.remove(cur.size()-1);//将当前值删除，以回溯
               return ;
       }else{
           dfs(res,cur,root.left,targetSum-root.val);
           dfs(res,cur,root.right,targetSum-root.val);
           cur.remove(cur.size()-1);//当前节点遍历结束，删除，以回溯
        }
    }
}
//上面都是减的版本，这个是加的版本，本质上没什么区别
class Solution {
    public List<List<Integer>> pathSum(TreeNode root, int targetSum) {
        List<List<Integer>> res = new ArrayList<List<Integer>>();
        List<Integer> cur = new ArrayList<Integer>();
        dfs(res,cur,root,targetSum,0);
        return res;
    }
    public void dfs(List<List<Integer>> res,List<Integer>cur,TreeNode root,int targetSum,int total){
       if(root==null)return ;
       cur.add(root.val);
       total+=root.val;
       if(root.left==null&&root.right==null&&total==targetSum){
               res.add(new ArrayList<Integer>(cur));
               cur.remove(cur.size()-1);
               return ;
       }else{
           dfs(res,cur,root.left,targetSum,total);
           dfs(res,cur,root.right,targetSum,total);
           cur.remove(cur.size()-1);
        }
    }
}
```

### [437. 路径总和 III](https://leetcode-cn.com/problems/path-sum-iii/)

给定一个二叉树，它的每个结点都存放着一个整数值。

找出路径和等于给定数值的路径总数。

路径不需要从根节点开始，也不需要在叶子节点结束，但是路径方向必须是向下的（只能从父节点到子节点）。

二叉树不超过1000个节点，且节点数值范围是 [-1000000,1000000] 的整数。

**示例：**

```
root = [10,5,-3,3,2,null,11,3,-2,null,1], sum = 8

      10
     /  \
    5   -3
   / \    \
  3   2   11
 / \   \
3  -2   1

返回 3。和等于 8 的路径有:

1.  5 -> 3
2.  5 -> 2 -> 1
3.  -3 -> 11
```

```java
//前缀和的概念 && HashMap
class Solution {
    public int pathSum(TreeNode root, int sum) {
        Map<Integer,Integer> prefixSumCount = new HashMap<>();
        prefixSumCount.put(0,1);
        return recursionPathSum(root,prefixSumCount,sum,0);
    }
    public int recursionPathSum(TreeNode node,Map<Integer,Integer>prefixSumCount,int target,int currSum){
        if(node==null)return 0;
        int res = 0;
        currSum+=node.val;
        res+=prefixSumCount.getOrDefault(currSum-target,0);
        prefixSumCount.put(currSum,prefixSumCount.getOrDefault(currSum,0)+1);
        res+=recursionPathSum(node.left,prefixSumCount,target,currSum);
        res+=recursionPathSum(node.right,prefixSumCount,target,currSum);
        prefixSumCount.put(currSum,prefixSumCount.get(currSum)-1);
        return res;
    }
}
```

### [563. 二叉树的坡度](https://leetcode-cn.com/problems/binary-tree-tilt/)

给定一个二叉树，计算 **整个树** 的坡度 。

一个树的 **节点的坡度** 定义即为，该节点左子树的节点之和和右子树节点之和的 **差的绝对值** 。如果没有左子树的话，左子树的节点之和为 0 ；没有右子树的话也是一样。空结点的坡度是 0 。

**整个树** 的坡度就是其所有节点的坡度之和。

 

**示例 1：**

![img](https://assets.leetcode.com/uploads/2020/10/20/tilt1.jpg)

```
输入：root = [1,2,3]
输出：1
解释：
节点 2 的坡度：|0-0| = 0（没有子节点）
节点 3 的坡度：|0-0| = 0（没有子节点）
节点 1 的坡度：|2-3| = 1（左子树就是左子节点，所以和是 2 ；右子树就是右子节点，所以和是 3 ）
坡度总和：0 + 0 + 1 = 1
```

**示例 2：**

![img](https://assets.leetcode.com/uploads/2020/10/20/tilt2.jpg)

```
输入：root = [4,2,9,3,5,null,7]
输出：15
解释：
节点 3 的坡度：|0-0| = 0（没有子节点）
节点 5 的坡度：|0-0| = 0（没有子节点）
节点 7 的坡度：|0-0| = 0（没有子节点）
节点 2 的坡度：|3-5| = 2（左子树就是左子节点，所以和是 3 ；右子树就是右子节点，所以和是 5 ）
节点 9 的坡度：|0-7| = 7（没有左子树，所以和是 0 ；右子树正好是右子节点，所以和是 7 ）
节点 4 的坡度：|(3+5+2)-(9+7)| = |10-16| = 6（左子树值为 3、5 和 2 ，和是 10 ；右子树值为 9 和 7 ，和是 16 ）
坡度总和：0 + 0 + 0 + 2 + 7 + 6 = 15
```

```java
//后序遍历
class Solution {
    public int res= 0;
    public int findTilt(TreeNode root) {
        if(root==null)return 0;
        dfs(root);
        return res;
    }
//答案的解法 自己没转过来   每一次递归做的事：计算当前节点的坡度累加到res中，向上返回该节点及其子节点的和，用于上一层节点的res计算
    public int dfs(TreeNode node){
        if(node==null)return 0;
        int left = dfs(node.left);
        int right = dfs(node.right);
        res+=Math.abs(left-right);
        return left+right+node.val;
    }
}
```

### [617. 合并二叉树](https://leetcode-cn.com/problems/merge-two-binary-trees/)

给定两个二叉树，想象当你将它们中的一个覆盖到另一个上时，两个二叉树的一些节点便会重叠。

你需要将他们合并为一个新的二叉树。合并的规则是如果两个节点重叠，那么将他们的值相加作为节点合并后的新值，否则**不为** NULL 的节点将直接作为新二叉树的节点。

**示例 1:**

```
输入: 
	Tree 1                     Tree 2                  
          1                         2                             
         / \                       / \                            
        3   2                     1   3                        
       /                           \   \                      
      5                             4   7                  
输出: 
合并后的树:
	     3
	    / \
	   4   5
	  / \   \ 
	 5   4   7
```

**注意:** 合并必须从两个树的根节点开始。

```java
//对root1进行操作的思维
class Solution {
    public TreeNode mergeTrees(TreeNode root1, TreeNode root2) {
        if(root1==null&&root2==null)return null;
        if(root1==null)root1 = root2;//一个细节 不能只是简单赋值，而应将root1的引用指向root2
        else if(root1!=null&&root2!=null){
            root1.val +=root2.val;
            root1.left = mergeTrees(root1.left,root2.left);
            root1.right = mergeTrees(root1.right,root2.right);
        }
        return root1;
    }
}
//参考答案的解法 更快 ---转换思维，不是对root1进行操作，而是在两个数的每一个相应节点上进行选取，成为一个新的节点并返回
class Solution {
    public TreeNode mergeTrees(TreeNode root1, TreeNode root2) {
        if(root1==null)return root2;
        if(root2==null)return root1;
        TreeNode cur = new TreeNode(root1.val+root2.val);
        cur.left = mergeTrees(root1.left,root2.left);
        cur.right = mergeTrees(root1.right,root2.right);
        return cur;
    }
}
```



## 树的层次遍历

### [102. 二叉树的层序遍历](https://leetcode-cn.com/problems/binary-tree-level-order-traversal/)

给你一个二叉树，请你返回其按 **层序遍历** 得到的节点值。 （即逐层地，从左到右访问所有节点）。

**示例：**
二叉树：`[3,9,20,null,null,15,7]`,

```
    3
   / \
  9  20
    /  \
   15   7
```

返回其层序遍历结果：

```
[
  [3],
  [9,20],
  [15,7]
]
```

```java
//迭代写法 
class Solution {
    public List<List<Integer>> levelOrder(TreeNode root) {
        List<List<Integer>>res = new ArrayList<>();
        Queue<TreeNode>queue = new LinkedList<>();
        if(root==null)return res;
        queue.offer(root);
        while(!queue.isEmpty()){
            List<Integer>cur = new ArrayList<>();
            int size = queue.size();//一个需要注意的小细节 如果写在for循环里会出错
            for(int i =1;i<=size;i++){
                TreeNode node = queue.poll();
                cur.add(node.val);
                if(node.left!=null)queue.offer(node.left);
                if(node.right!=null)queue.offer(node.right);
            }
            res.add(cur);
        }
        return res;
    }
}
//递归的方法，深度优先遍历
class Solution {
    public List<List<Integer>> levelOrder(TreeNode root) {
        List<List<Integer>> res = new ArrayList<>();
        if(root==null)return res;
        dfs(1,root,res);
        return res;
    }
    public void dfs(int index,TreeNode node,List<List<Integer>> res){
        if(res.size()<index)res.add(new ArrayList<>());
        res.get(index-1).add(node.val);
        if(node.left!=null)dfs(index+1,node.left,res);
        if(node.right!=null)dfs(index+1,node.right,res);
    }
}
```

### [429. N 叉树的层序遍历](https://leetcode-cn.com/problems/n-ary-tree-level-order-traversal/)

给定一个 N 叉树，返回其节点值的*层序遍历*。（即从左到右，逐层遍历）。

树的序列化输入是用层序遍历，每组子节点都由 null 值分隔（参见示例）。

 

**示例 1：**

![img](https://assets.leetcode.com/uploads/2018/10/12/narytreeexample.png)

```
输入：root = [1,null,3,2,4,null,5,6]
输出：[[1],[3,2,4],[5,6]]
```

**示例 2：**

![img](https://assets.leetcode.com/uploads/2019/11/08/sample_4_964.png)

```
输入：root = [1,null,2,3,4,5,null,null,6,7,null,8,null,9,10,null,null,11,null,12,null,13,null,null,14]
输出：[[1],[2,3,4,5],[6,7,8,9,10],[11,12,13],[14]]
```

```java
//同样广度优先遍历，套用模板就ok了
class Solution {
    public List<List<Integer>> levelOrder(Node root) {
        List<List<Integer>> res =new ArrayList<>();
        if(root==null)return res;
        Queue<Node>queue = new LinkedList<>();
        queue.add(root);
        while(!queue.isEmpty()){
            List<Integer>cur = new ArrayList<>();
            int size = queue.size();
            for(int i =0;i<size;i++){
                Node node = queue.poll();
                cur.add(node.val);
                for(Node child:node.children){//与上一题仅在此处有变化
                    if(child!=null)queue.add(child);
                }
            }
            res.add(cur);
        }
        return res;
    }
}
//同样的深度优先 套用模板
class Solution {
    public List<List<Integer>> levelOrder(Node root) {
        List<List<Integer>> res =new ArrayList<>();
        if(root==null)return res;
        dfs(1,root,res);
        return res;
    }
    public void dfs(int index,Node node,List<List<Integer>> res){
        if(res.size()<index) res.add(new ArrayList<>());
        if(node!=null) res.get(index-1).add(node.val);
        for(Node child:node.children){
            dfs(index+1,child,res);
        }
    }
}
```



### [690. 员工的重要性](https://leetcode-cn.com/problems/employee-importance/)

给定一个保存员工信息的数据结构，它包含了员工**唯一的id**，**重要度** 和 **直系下属的id**。

比如，员工1是员工2的领导，员工2是员工3的领导。他们相应的重要度为15, 10, 5。那么员工1的数据结构是[1, 15, [2]]，员工2的数据结构是[2, 10, [3]]，员工3的数据结构是[3, 5, []]。注意虽然员工3也是员工1的一个下属，但是由于**并不是直系**下属，因此没有体现在员工1的数据结构中。

现在输入一个公司的所有员工信息，以及单个员工id，返回这个员工和他所有下属的重要度之和。

**示例 1:**

```
输入: [[1, 5, [2, 3]], [2, 3, []], [3, 3, []]], 1
输出: 11
解释:
员工1自身的重要度是5，他有两个直系下属2和3，而且2和3的重要度均为3。因此员工1的总重要度是 5 + 3 + 3 = 11。
```

**注意:**

1. 一个员工最多有一个**直系**领导，但是可以有多个**直系**下属
2. 员工数量不超过2000。

```java
//BFS 在基本框架的基础上添加HashMap用来实现员工id和员工类的映射
class Solution {
    public int getImportance(List<Employee> employees, int id) {
        int count = 0;
        Map<Integer,Employee>map = new HashMap<>();
        for(Employee employee:employees){
            map.put(employee.id,employee);
        }
        Queue<Integer>queue = new LinkedList<>();
        queue.add(id);
        while(!queue.isEmpty()){
            int cur = queue.poll();
            Employee curEmp = map.get(cur);
            count+=curEmp.importance;
            for(Integer iid:curEmp.subordinates){
                queue.add(iid);
            }
        }
        return count;
    }
}
//另一种小变形，queue存储的直接为Employee，这样用起来更方便，耗时也更少。
        Queue<Employee>queue = new LinkedList<>();
        queue.add(map.get(id));
        while(!queue.isEmpty()){
            Employee curEmp = queue.poll();
            count+=curEmp.importance;
            for(Integer iid:curEmp.subordinates){
                queue.add(map.get(iid));
            }
//DFS 这里需要注意count的声明不应写在getImportance方法体内成为局部变量，应该声明为全局变量，否则count的值不会发生变化。
class Solution {
    public int count = 0;
    public int getImportance(List<Employee> employees, int id) {
        Map<Integer,Employee>map = new HashMap<>();
        for(Employee employee:employees){
            map.put(employee.id,employee);
        }
        dfs(map,id);
        return count;
    }
    public void dfs(Map<Integer,Employee>map,int id){
        Employee curEmp = map.get(id);
        count+=curEmp.importance;
        for(Integer subId:curEmp.subordinates){
            dfs(map,subId);
        }
    }
}
```

### [559. N 叉树的最大深度](https://leetcode-cn.com/problems/maximum-depth-of-n-ary-tree/)

给定一个 N 叉树，找到其最大深度。

最大深度是指从根节点到最远叶子节点的最长路径上的节点总数。

N 叉树输入按层序遍历序列化表示，每组子节点由空值分隔（请参见示例）。

 

**示例 1：**

![img](https://assets.leetcode.com/uploads/2018/10/12/narytreeexample.png)

```
输入：root = [1,null,3,2,4,null,5,6]
输出：3
```

**示例 2：**

![img](https://assets.leetcode.com/uploads/2019/11/08/sample_4_964.png)

```
输入：root = [1,null,2,3,4,5,null,null,6,7,null,8,null,9,10,null,null,11,null,12,null,13,null,null,14]
输出：5 
```

**提示：**

- 树的深度不会超过 `1000` 。
- 树的节点数目位于 `[0, 104]` 之间。

```java
//简单的DFS遍历
class Solution {
    public int maxDepth(Node root) {
        if(root==null)return 0;
        int maxCur=0;
        for(Node child:root.children){
            maxCur = Math.max(maxCur,maxDepth(child));
        }
        return maxCur+1;
    }
}
//简单的BFS遍历
class Solution {
    public int maxDepth(Node root) {
        int depth = 0;
        if(root==null)return depth;
        Queue<Node>queue = new LinkedList<>();
        queue.add(root);
        while(!queue.isEmpty()){
            int size = queue.size();
            for(int i=0;i<size;i++){
                Node cur = queue.poll();
                for(Node child:cur.children){
                    if(child!=null)queue.add(child);
                }
            }
            depth++;
        }
        return depth;
    }
}
```



### [662. 二叉树最大宽度](https://leetcode-cn.com/problems/maximum-width-of-binary-tree/)

给定一个二叉树，编写一个函数来获取这个树的最大宽度。树的宽度是所有层中的最大宽度。这个二叉树与**满二叉树（full binary tree）**结构相同，但一些节点为空。

每一层的宽度被定义为两个端点（该层最左和最右的非空节点，两端点间的`null`节点也计入长度）之间的长度。

**示例 1:**

```
输入: 

           1
         /   \
        3     2
       / \     \  
      5   3     9 

输出: 4
解释: 最大值出现在树的第 3 层，宽度为 4 (5,3,null,9)。
```

**示例 2:**

```
输入: 

          1
         /  
        3    
       / \       
      5   3     

输出: 2
解释: 最大值出现在树的第 3 层，宽度为 2 (5,3)。
```

**示例 3:**

```
输入: 

          1
         / \
        3   2 
       /        
      5      

输出: 2
解释: 最大值出现在树的第 2 层，宽度为 2 (3,2)。
```

**示例 4:**

```
输入: 

          1
         / \
        3   2
       /     \  
      5       9 
     /         \
    6           7
输出: 8
解释: 最大值出现在树的第 4 层，宽度为 8 (6,null,null,null,null,null,null,7)。
```

**注意:** 答案在32位有符号整数的表示范围内。

```java
//自己没想起来，这是官方的解法
class Solution {
    public int widthOfBinaryTree(TreeNode root) {
        if(root==null)return 0;
        Node node = new Node(root,1,1);//设为1后就理解了  奥利给
        Queue<Node>queue = new LinkedList<>();
        queue.add(node);
        int Depth = 0;
        int res = 0;
        int left = 0;
        while(!queue.isEmpty()){
            int size = queue.size();
            for(int i =0;i<size;i++){
                Node cur = queue.poll();
                if(cur.node.left!=null){
                    queue.add(new Node(cur.node.left,cur.position*2,cur.depth+1));
                }
                if(cur.node.right!=null){
                    queue.add(new Node(cur.node.right,cur.position*2+1,cur.depth+1));
                }     
                if(Depth<cur.depth){
                    Depth = cur.depth;
                    left = cur.position;
                }
                res = Math.max(res,cur.position-left+1);//核心
            }
            
        }
        return res; 

}  
//定义了一个新的类用来存储位置和深度。。。
    class Node{
        TreeNode node;
        int position;
        int depth;
        public Node(TreeNode node,int position,int depth){
            this.node = node;
            this.position = position;
            this.depth = depth;
        }
    }
}
//评论区中的投机取巧的方法，因为node的val没有用处不如用来存储position了！牛逼
class Solution {
    public int widthOfBinaryTree(TreeNode root) {
        if(root==null)return 0;
        Deque<TreeNode>queue = new LinkedList<>();//用到了双端队列，便于调用getLast()和getFirst()方法
        root.val = 1;//根节点的position为1
        queue.add(root);
        int res = 0;
        while(!queue.isEmpty()){
            res = Math.max(res,queue.getLast().val-queue.getFirst().val+1);//getLast()和getFirst()
            int size = queue.size();
            for(int i =0;i<size;i++){
                TreeNode cur = queue.poll();
                if(cur.left!=null){
                    cur.left.val = cur.val*2;//左：2*val 右 2*val+1
                    queue.add(cur.left);
                }
                if(cur.right!=null){
                    queue.add(cur.right);
                    cur.right.val = cur.val*2+1;
                }
            }
            }
        return res;
        }
} 
//自己写的DFS 参考了别人的思路
class Solution {
    int []left = new int [3000];//开了很大 评论区有用HashMap的
    int Depth = 0;
    int res = 0;
    public int widthOfBinaryTree(TreeNode root) {
        if(root==null)return 0;
        dfs(root,1,1);
        return res;
    }
    public void dfs(TreeNode root,int position,int depth){
        if(Depth<depth){
            Depth+=1;
            left[Depth] = position;
        }
        res=  Math.max(res,position-left[depth]+1);
        if(root.left!=null)dfs(root.left,position*2,depth+1);
        if(root.right!=null)dfs(root.right,position*2+1,depth+1);
    }
}
```

### [111. 二叉树的最小深度](https://leetcode-cn.com/problems/minimum-depth-of-binary-tree/)

给定一个二叉树，找出其最小深度。

最小深度是从根节点到最近叶子节点的最短路径上的节点数量。

**说明：**叶子节点是指没有子节点的节点。

 

**示例 1：**

![img](https://assets.leetcode.com/uploads/2020/10/12/ex_depth.jpg)

```
输入：root = [3,9,20,null,null,15,7]
输出：2
```

```java
//算法小抄上的例题，借助BFS框架 对于求最短路径这类问题比较合适。  由一个点开始，发散，起步并进。要求空间复杂度可能会更高些。  体会DFS并没有这种思想。
class Solution {
    public int minDepth(TreeNode root) {
        if(root==null)return 0;
        int depth = 1;
        Queue<TreeNode>queue = new LinkedList<>();
        queue.add(root);
        while(!queue.isEmpty()){
            int size = queue.size();
            for(int i=0;i<size;i++){
                TreeNode cur = queue.poll();
                if(cur.left==null&&cur.right==null)return depth;
                if(cur.left!=null)queue.add(cur.left);
                if(cur.right!=null)queue.add(cur.right);
            }
            depth++;
        }
        return 0;
    }
}
//当然这个题也可以用DFS去做
class Solution {
    public int res = Integer.MAX_VALUE;
    public int minDepth(TreeNode root) {
       if(root==null) return 0;
       dfs(root,1);
       return res;
    }
    public void dfs(TreeNode cur,int depth){
        if(cur.left==null&&cur.right==null){
            res = Math.min(res,depth);
            return ;
        }
        if(cur.left!=null) dfs(cur.left,depth+1);
        if(cur.right!=null)dfs(cur.right,depth+1);
    }
}
```

### [752. 打开转盘锁](https://leetcode-cn.com/problems/open-the-lock/)

你有一个带有四个圆形拨轮的转盘锁。每个拨轮都有10个数字： `'0', '1', '2', '3', '4', '5', '6', '7', '8', '9'` 。每个拨轮可以自由旋转：例如把 `'9'` 变为 `'0'`，`'0'` 变为 `'9'` 。每次旋转都只能旋转一个拨轮的一位数字。

锁的初始数字为 `'0000'` ，一个代表四个拨轮的数字的字符串。

列表 `deadends` 包含了一组死亡数字，一旦拨轮的数字和列表里的任何一个元素相同，这个锁将会被永久锁定，无法再被旋转。

字符串 `target` 代表可以解锁的数字，你需要给出最小的旋转次数，如果无论如何不能解锁，返回 -1。

**示例 1:**

```
输入：deadends = ["0201","0101","0102","1212","2002"], target = "0202"
输出：6
解释：
可能的移动序列为 "0000" -> "1000" -> "1100" -> "1200" -> "1201" -> "1202" -> "0202"。
注意 "0000" -> "0001" -> "0002" -> "0102" -> "0202" 这样的序列是不能解锁的，
因为当拨动到 "0102" 时这个锁就会被锁定。
```

**示例 2:**

```
输入: deadends = ["8888"], target = "0009"
输出：1
解释：
把最后一位反向旋转一次即可 "0000" -> "0009"。
```

**示例 3:**

```
输入: deadends = ["8887","8889","8878","8898","8788","8988","7888","9888"], target = "8888"
输出：-1
解释：
无法旋转到目标数字且不被锁定。
```

**示例 4:**

```
输入: deadends = ["0000"], target = "8888"
输出：-1
```

```java
//算法小抄上的BFS的题目，基于BFS框架，更复杂些，也学到了许多新东西 如HashSet来检查是否visited和违反限定条件 、字符串的转换操作。
class Solution {
    public String plusOne(String str,int index){
        StringBuilder sb = new StringBuilder(str);
        char c = sb.charAt(index);
        if(c=='9'){
            c = '0';
        }else {
            c = (char)(c+1);
        }
        sb.setCharAt(index,c);
        return sb.toString();
    }
    public String minusOne(String str,int index){
        StringBuilder sb = new StringBuilder(str);
        char c = sb.charAt(index);
        if(c=='0'){
            c = '9';
        }else {
            c = (char)(c-1);
        }
        sb.setCharAt(index,c);
        return sb.toString();
    }
    public int openLock(String[] deadends, String target) {
        Set<String>deads = new HashSet<>();
        for(String dead:deadends){
            deads.add(dead);
        }
        Set<String>visited = new HashSet<>();
        Queue<String>queue = new LinkedList<>();
        int step = 0;
        queue.add("0000");
        visited.add("0000");
        while(!queue.isEmpty()){
            int size = queue.size();
            for(int i=0;i<size;i++){
                String cur = queue.poll();
                if(deads.contains(cur))continue;
                if(target.equals(cur))return step;
                for(int index=0;index<4;index++){
                    String tmp1 = plusOne(cur,index);
                    String tmp2 = minusOne(cur,index);
                    if(!visited.contains(tmp1)){
                        queue.add(tmp1);
                        visited.add(tmp1);
                    }
                    if(!visited.contains(tmp2)){
                        queue.add(tmp2);
                        visited.add(tmp2);
                    }
                }
            }
            step++;
        }
        return -1;
    }
}
```

## 数的前序遍历

### [144. 二叉树的前序遍历](https://leetcode-cn.com/problems/binary-tree-preorder-traversal/)

给你二叉树的根节点 `root` ，返回它节点值的 **前序** 遍历。

 

**示例 1：**

![img](https://assets.leetcode.com/uploads/2020/09/15/inorder_1.jpg)

```
输入：root = [1,null,2,3]
输出：[1,2,3]
```

```JAVA
//递归
class Solution {
    public List<Integer>res = new ArrayList<>();
    public List<Integer> preorderTraversal(TreeNode root) {
        dfs(root);
        return res;
    }   
    public void dfs(TreeNode node){
        if(node==null)return;
        if(node!=null)res.add(node.val);
        dfs(node.left);
        dfs(node.right);
    }
}
//迭代
class Solution {
    public List<Integer> preorderTraversal(TreeNode root) {
        List<Integer>res = new ArrayList<>();
        if(root==null)return res;
        Deque<TreeNode> stack = new LinkedList<>();
        stack.addLast(root);
        while(!stack.isEmpty()){
            TreeNode cur = stack.removeLast();
            res.add(cur.val);
            if(cur.right!=null) stack.addLast(cur.right);//先右后左
            if(cur.left!=null)stack.addLast(cur.left);//先右后左
        }
        return res;
    }   
}
```

### [589. N叉树的前序遍历](https://leetcode-cn.com/problems/n-ary-tree-preorder-traversal/)

给定一个 N 叉树，返回其节点值的*前序遍历*。

例如，给定一个 `3叉树` :

 

![img](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2018/10/12/narytreeexample.png)

 

返回其前序遍历: `[1,3,5,6,2,4]`。

 ```java
//递归
class Solution {
    public List<Integer>list = new ArrayList<Integer>();
    public List<Integer> preorder(Node root) {
        preorder_(root);
        return list;
    }
    public void preorder_(Node p){
        if(p==null)return ;
        list.add(p.val);
        for(Node children:p.children){
            preorder_(children);
        }
    }
}


//迭代
class Solution {
    public List<Integer> preorder(Node root) {
        List<Integer>res = new ArrayList<>();
        if(root==null)return res;
        Deque<Node>stack = new LinkedList<>();
        stack.addLast(root);
        while(!stack.isEmpty()){
            Node cur = stack.removeLast();
            res.add(cur.val);
            for(int i=cur.children.size()-1;i>=0;i--){
                Node child = cur.children.get(i);
                if(child!=null) stack.addLast(child);
            }  
        }
        return res;
    }
}
//迭代版本二  使用Collections.reverse方法
class Solution {
    public List<Integer> preorder(Node root) {
          LinkedList<Node> stack = new LinkedList<Node>();
          LinkedList<Integer>outputs = new LinkedList<Integer>();
          if(root==null) return outputs;
         stack.add(root);
         while(!stack.isEmpty()){
             Node node = stack.pollLast();
             outputs.add(node.val);
             Collections.reverse(node.children);
             for(Node child:node.children){
                 stack.add(child);
             }
            }
            return outputs;
         }
}
 ```



## **树的中序遍历与二叉搜索树**

### [94. 二叉树的中序遍历](https://leetcode-cn.com/problems/binary-tree-inorder-traversal/)

给定一个二叉树的根节点 `root` ，返回它的 **中序** 遍历。

```java
//递归
class Solution {
    public List<Integer>res = new ArrayList<>();
    public List<Integer> inorderTraversal(TreeNode root) {
        if(root==null)return res;
        middleTraverse(root);
        return res;
    }
    public void middleTraverse(TreeNode node){
        if(node.left!=null)middleTraverse(node.left);
        res.add(node.val);
        if(node.right!=null)middleTraverse(node.right);
    }
}
//迭代 使用栈
class Solution {
    public List<Integer> inorderTraversal(TreeNode root) {
        List<Integer> res = new ArrayList<>();
        if(root==null)return res;
        Deque<TreeNode> stack = new LinkedList<>();
        while(root!=null||!stack.isEmpty()){
            while(root!=null){
                stack.push(root);
                root = root.left;
            }
            root = stack.pop();
            res.add(root.val);
            root = root.right;
        }
        return res;
    }
}
```



### [700. 二叉搜索树中的搜索](https://leetcode-cn.com/problems/search-in-a-binary-search-tree/)

给定二叉搜索树（BST）的根节点和一个值。 你需要在BST中找到节点值等于给定值的节点。 返回以该节点为根的子树。 如果节点不存在，则返回 NULL。

例如，

```
给定二叉搜索树:

        4
       / \
      2   7
     / \
    1   3

和值: 2
```

你应该返回如下子树:

```
      2     
     / \   
    1   3
```

在上述示例中，如果要找的值是 `5`，但因为没有节点值为 `5`，我们应该返回 `NULL`。

```java
//递归
class Solution {
    public TreeNode searchBST(TreeNode root, int val) {
        if(root==null) return null;
        if(root.val ==val)return root;
        if(root.val>val)return searchBST(root.left,val);
        return searchBST(root.right,val);
    }
}
//迭代
class Solution {
    public TreeNode searchBST(TreeNode root, int val) {
        while(root!=null){
            if(root.val==val)return root;
            else if(root.val>val) root = root.left;
            else root = root.right;
        }
        return null;
    }
}
```

### [530. 二叉搜索树的最小绝对差](https://leetcode-cn.com/problems/minimum-absolute-difference-in-bst/)

给你一棵所有节点为非负值的二叉搜索树，请你计算树中任意两节点的差的绝对值的最小值。 

**示例：**

```
输入：

   1
    \
     3
    /
   2

输出：
1

解释：
最小绝对差为 1，其中 2 和 1 的差的绝对值为 1（或者 2 和 3）。
```

```java
//中序遍历
class Solution {
    public int res = Integer.MAX_VALUE;
    public Integer pre;
    public int getMinimumDifference(TreeNode root) {
        dfs(root);
        return res;
    }
    public void dfs(TreeNode node){
        if(node==null)return ;
        dfs(node.left);
        if(pre!=null)res = Math.min(res,Math.abs(node.val-pre));
        pre = node.val;
        dfs(node.right);
    }
}
//中序遍历 保存到数组中
class Solution {
    public List<Integer> list;
    public int getMinimumDifference(TreeNode root) {
        int res = Integer.MAX_VALUE;
        list = new ArrayList<>();
        dfs(root);
        for(int i =0;i<list.size()-1;i++){
            res = Math.min(res,Math.abs(list.get(i)-list.get(i+1)));
        }
        return res;
    }
    public void dfs(TreeNode node){
        if(node==null)return ;
        dfs(node.left);
        list.add(node.val);
        dfs(node.right);
    }
}
```

### [538. 把二叉搜索树转换为累加树](https://leetcode-cn.com/problems/convert-bst-to-greater-tree/)

给出二叉 **搜索** 树的根节点，该树的节点值各不相同，请你将其转换为累加树（Greater Sum Tree），使每个节点 `node` 的新值等于原树中大于或等于 `node.val` 的值之和。

提醒一下，二叉搜索树满足下列约束条件：

- 节点的左子树仅包含键 **小于** 节点键的节点。
- 节点的右子树仅包含键 **大于** 节点键的节点。
- 左右子树也必须是二叉搜索树。

```java
//变形的中序遍历
class Solution {
    public Integer pre;
    public TreeNode convertBST(TreeNode root) {
        dfs(root);
        return root;
    }
    public void dfs(TreeNode node){
        if(node==null)return ;
        dfs(node.right);
        if(pre!=null){
            node.val +=pre;
        }
        pre = node.val;
        dfs(node.left);
    }
}
```

### [230. 二叉搜索树中第K小的元素](https://leetcode-cn.com/problems/kth-smallest-element-in-a-bst/)

给定一个二叉搜索树的根节点 `root` ，和一个整数 `k` ，请你设计一个算法查找其中第 `k` 个最小元素（从 1 开始计数）。

 

**示例 1：**

![img](https://assets.leetcode.com/uploads/2021/01/28/kthtree1.jpg)

```
输入：root = [3,1,4,null,2], k = 1
输出：1
```

**示例 2：**

![img](https://assets.leetcode.com/uploads/2021/01/28/kthtree2.jpg)

```
输入：root = [5,3,6,2,4,null,null,1], k = 3
输出：3
```

**提示：**

- 树中的节点数为 `n` 。
- `1 <= k <= n <= 104`
- `0 <= Node.val <= 104`

```java
class Solution {
    public int index = 0;
    public int res;
    public int kthSmallest(TreeNode root, int k) {
        dfs(root,k);
        return res;
    }
    public void dfs(TreeNode node,int k){
        if(node==null)return ;
        dfs(node.left,k);
        index++;
        if(index==k){
          res = node.val;
          return;
        }
        dfs(node.right,k);
    }
}
```

### [98. 验证二叉搜索树](https://leetcode-cn.com/problems/validate-binary-search-tree/)

给定一个二叉树，判断其是否是一个有效的二叉搜索树。

假设一个二叉搜索树具有如下特征：

- 节点的左子树只包含**小于**当前节点的数。
- 节点的右子树只包含**大于**当前节点的数。
- 所有左子树和右子树自身必须也是二叉搜索树。

```java
//比较慢的方法
class Solution {
    public List<Integer> res = new ArrayList<>();
    public boolean isValidBST(TreeNode root) {
        if(root==null)return true;
        dfs(root);
        for(int i =0;i<res.size()-1;i++){
            if(res.get(i)>=res.get(i+1))return false;
        }
        return true;
        
    }
    public void dfs(TreeNode node){
        if(node==null) return;
        dfs(node.left);
        res.add(node.val);
        dfs(node.right);
    }
}
//使用pre保存前面那个数
class Solution {
    public Integer pre;
    public boolean flag = true;
    public boolean isValidBST(TreeNode root) {
        if(root==null)return true;
        dfs(root);
        return flag;
    }
    public void dfs(TreeNode node){
        if(node==null) return;
        dfs(node.left);
        if(pre!=null){
            if(pre>=node.val){
                flag=false;
                return;
            }
        }
        pre = node.val;
        dfs(node.right);
    }
}
```

## 重构二叉树

### [105. 从前序与中序遍历序列构造二叉树](https://leetcode-cn.com/problems/construct-binary-tree-from-preorder-and-inorder-traversal/)

根据一棵树的前序遍历与中序遍历构造二叉树。

**注意:**
你可以假设树中没有重复的元素。

例如，给出

```
前序遍历 preorder = [3,9,20,15,7]
中序遍历 inorder = [9,3,15,20,7]
```

返回如下的二叉树：

```
    3
   / \
  9  20
    /  \
   15   7
```

```java
//迭代 经典题目
class Solution {
    public Map<Integer,Integer> indexMap;//中序遍历的 值-位置映射
    public TreeNode buildTree(int[] preorder, int[] inorder) {
        indexMap = new HashMap<>();
        int n = inorder.length;
        for(int i=0;i<n;i++){
            indexMap.put(inorder[i],i);
        }
        return MyBuildTree(preorder,inorder,0,n-1,0,n-1);
    }

    public TreeNode MyBuildTree(int []preorder,int []inorder,int pre_left,int pre_right,int in_left,int in_right){
        if(pre_left>pre_right)return null;//越界检查 
      // 也可以是 if(in_left>in_right||pre_left>pre_right)return null;
        int root_num = preorder[pre_left];
        int in_index = indexMap.get(root_num);
        TreeNode root = new TreeNode(root_num);
        int left_size = in_index-in_left;
        root.left = MyBuildTree(preorder,inorder,pre_left+1,pre_left+left_size,in_left,in_index-1);
        root.right= MyBuildTree(preorder,inorder,pre_left+left_size+1,pre_right,in_index+1,in_right);
        return root;
    }
}
```

### [106. 从中序与后序遍历序列构造二叉树](https://leetcode-cn.com/problems/construct-binary-tree-from-inorder-and-postorder-traversal/)

根据一棵树的中序遍历与后序遍历构造二叉树。

**注意:**
你可以假设树中没有重复的元素。

例如，给出

```
中序遍历 inorder = [9,3,15,20,7]
后序遍历 postorder = [9,15,7,20,3]
```

返回如下的二叉树：

```
    3
   / \
  9  20
    /  \
   15   7
```

```java
//总结一下 这两个题的关键点就是在于左右子树的left和right边界索引的确定
//感觉自己的思维能力提升了哈哈
class Solution {
    public Map<Integer,Integer> indexMap;//中序遍历的 值-位置映射
    public TreeNode buildTree(int[] inorder, int[] postorder) {
        indexMap = new HashMap<>();
        int n = inorder.length;
        for(int i=0;i<n;i++){
            indexMap.put(inorder[i],i);
        }
        return MyBuildTree(postorder,inorder,0,n-1,0,n-1);
    }
    public TreeNode MyBuildTree(int []postorder,int []inorder,int post_left,int post_right,int in_left,int in_right){
        if(in_left>in_right)return null;//越界检查 
        int root_num = postorder[post_right];
        int in_index = indexMap.get(root_num);
        TreeNode root = new TreeNode(root_num);
        int left_size = in_index-in_left;
        root.left = MyBuildTree(postorder,inorder,post_left,post_left+left_size-1,in_left,in_index-1);
        root.right= MyBuildTree(postorder,inorder,post_left+left_size,post_right-1,in_index+1,in_right);
        return root;
    }
}
```



## 树的后序遍历

### [145. 二叉树的后序遍历](https://leetcode-cn.com/problems/binary-tree-postorder-traversal/)

给定一个二叉树，返回它的 *后序* 遍历。

**示例:**

```
输入: [1,null,2,3]  
   1
    \
     2
    /
   3 

输出: [3,2,1]
```

**进阶:** 递归算法很简单，你可以通过迭代算法完成吗？

```java
//递归
class Solution {
    public List<Integer> postorderTraversal(TreeNode root) {
        List<Integer>res =new ArrayList<>();
        dfs(res,root);
        return res;
    }
    public void dfs(List<Integer>res,TreeNode node){
        if(node==null)return ;
        dfs(res,node.left);
        dfs(res,node.right);
        res.add(node.val);
    }
}
//迭代 有些不太好理解 特别是visited的使用
class Solution {
    public List<Integer> postorderTraversal(TreeNode root) {
        List<Integer>res = new ArrayList<>();
        if(root==null)return res;
        TreeNode visted=null;
        Deque<TreeNode>stack = new LinkedList<>();
        while(!stack.isEmpty()||root!=null){
            while(root!=null){
                stack.push(root);
                root = root.left;
            }
            root = stack.poll();
            if(root.right==null||root.right==visted){
                res.add(root.val);
                visted = root;
                root = null;
            }else{
                stack.push(root);
                root = root.right;
            }
        }
        return res;
    }
}
//评论区的解法 看起来很棒 但自己现在脑子不转了感觉
//关于stack的add和remove 经过测试，同一使用addFirst removeFirst或addLast removeLast 结果都是可以的
//所以这个解法的关键点在于ans的add操作始终都是在开头进行添加元素
class Solution {
    public List<Integer> postorderTraversal(TreeNode root) {
        Deque<TreeNode> stack = new LinkedList<>();
        LinkedList<Integer> ans = new LinkedList<>();
        if (null == root) return ans;
        stack.addFirst(root);
        while(!stack.isEmpty()) {
            TreeNode node = stack.removeFirst();
            ans.addFirst(node.val);
            if (node.left!=null) {
                stack.addFirst(node.left);
            }
            if (node.right!=null) {
                stack.addFirst(node.right);
            }
        }
        return ans;
    }
}
```







**十. 图与搜索**

题目分类	题目编号
图的建立与应用	565
深度优先搜索	17、397
回溯法	526、401、36、37、51、52、77、39、216、40、46、47、31、556、60、491、78、90、79、93、332
回溯法与表达式	241、282、679
回溯法与括号	22、301
回溯法与贪心	488
广度优先搜索	133、200、695、463、542、130、417、529、127、126、433、675
并查集	547、684、685
拓扑排序	399、207、210
有限状态自动机	65、468

## **十.图与搜索**

### 回溯法

### [46. 全排列](https://leetcode-cn.com/problems/permutations/)

给定一个 **没有重复** 数字的序列，返回其所有可能的全排列。

**示例:**

```
输入: [1,2,3]
输出:
[
  [1,2,3],
  [1,3,2],
  [2,1,3],
  [2,3,1],
  [3,1,2],
  [3,2,1]
]
```

```JAVA
class Solution {
    public List<List<Integer>>res = new ArrayList<>();
    public List<List<Integer>> permute(int[] nums) {
        List<Integer>track = new ArrayList<>();
        backtrack(track,nums);
        return res;
    }
    public void backtrack(List<Integer>track,int[]nums){
        if(track.size()==nums.length){
            res.add(new ArrayList(track));
            return;
        }
        for(int i =0;i<nums.length;i++){
            if(track.contains(nums[i])) continue;
            track.add(nums[i]);
            backtrack(track,nums);
            track.remove(track.size()-1);
        }
    }
}
```

### [51. N 皇后](https://leetcode-cn.com/problems/n-queens/)

**n 皇后问题** 研究的是如何将 `n` 个皇后放置在 `n×n` 的棋盘上，并且使皇后彼此之间不能相互攻击。

给你一个整数 `n` ，返回所有不同的 **n 皇后问题** 的解决方案。

每一种解法包含一个不同的 **n 皇后问题** 的棋子放置方案，该方案中 `'Q'` 和 `'.'` 分别代表了皇后和空位。

 

**示例 1：**

![img](https://assets.leetcode.com/uploads/2020/11/13/queens.jpg)

```
输入：n = 4
输出：[[".Q..","...Q","Q...","..Q."],["..Q.","Q...","...Q",".Q.."]]
解释：如上图所示，4 皇后问题存在两个不同的解法。
```

**示例 2：**

```
输入：n = 1
输出：[["Q"]]
```

```java
class Solution {
    public List<List<String>>res = new ArrayList<>();
    public List<List<String>> solveNQueens(int n) {
        char [][] board = new char[n][n];
        for(int i=0;i<n;i++){
            for(int j=0;j<n;j++){
                board[i][j] = '.';
            }
        }
        backTrack(board,0);
        return res;
    }
    public void backTrack(char[][]board,int row){
        if(row==board.length){
            List<String>track = char2List(board);
            res.add(track);
            return ;
        }
        for(int i=0;i<board[row].length;i++){
            if(!Valid(board,row,i)) continue;
            board[row][i] = 'Q';
            backTrack(board,row+1);
            board[row][i] = '.';
        }
    }
    public boolean Valid(char[][]board,int row,int col){
        for(int i =0;i<row;i++){
            if(board[i][col]=='Q')return false;
        }
        for(int i=row-1,j=col+1;i>=0&&j<board[0].length;i--,j++){
            if(board[i][j]=='Q')return false;
        }
        for(int i=row-1,j=col-1;i>=0&&j>=0;i--,j--){
            if(board[i][j]=='Q')return false;
        }
        return true;
    }

    public List<String>char2List(char [][]board){
        List<String> track = new ArrayList<>();
        for(int i=0;i<board.length;i++){
            track.add(new String(board[i]));
        }
        return track;
    }
}
```



## **十一. 二分查找**

题目分类	题目编号
二分查找应用(简单)	374、35、278、367、69、441
二分查找应用(中等)	34、540、275、436、300、354、658、162、4
二分查找与旋转数组	153、154、33、81
二分查找与矩阵	74、240
二分答案法	378、668、410、483

### [34. 在排序数组中查找元素的第一个和最后一个位置](https://leetcode-cn.com/problems/find-first-and-last-position-of-element-in-sorted-array/)

给定一个按照升序排列的整数数组 `nums`，和一个目标值 `target`。找出给定目标值在数组中的开始位置和结束位置。

如果数组中不存在目标值 `target`，返回 `[-1, -1]`。

**进阶：**

- 你可以设计并实现时间复杂度为 `O(log n)` 的算法解决此问题吗？

 

**示例 1：**

```
输入：nums = [5,7,7,8,8,10], target = 8
输出：[3,4]
```

**示例 2：**

```
输入：nums = [5,7,7,8,8,10], target = 6
输出：[-1,-1]
```

**示例 3：**

```
输入：nums = [], target = 0
输出：[-1,-1]
```

**提示：**

- `0 <= nums.length <= 105`
- `-109 <= nums[i] <= 109`
- `nums` 是一个非递减数组
- `-109 <= target <= 109`

```java
class Solution {
    public int[] searchRange(int[] nums, int target) {
        int start = getFirstK(nums,target,0,nums.length-1);
        int end = getLastK(nums,target,0,nums.length-1);
        int []res = new int[2];
        res[0] = start;
        res[1] = end;
        return res;
    }
    public int getFirstK(int []nums,int target,int left,int right){
        if(left>right)return -1;
        int middle = (left+right)/2;
        int cur =  nums[middle];
        if(cur==target){
            if(middle==0||nums[middle-1]!=target){
                return middle;
            }else{
                right = middle-1;
            }
        }else if(cur>target){
            right = middle-1;
        }else if(cur<target){
            left = middle +1;
        }
        return getFirstK(nums,target,left,right);
    }
    public int getLastK(int []nums,int target,int left,int right){
        if(left>right)return -1;
        int middle = (left+right)/2;
        int cur =  nums[middle];
        if(cur==target){
            if(middle==nums.length-1||nums[middle+1]!=target){
                return middle;
            }else{
                left = middle+1;
            }
        }else if(cur>target){
            right = middle-1;
        }else if(cur<target){
            left = middle +1;
        }
        return getLastK(nums,target,left,right);
    }
}
```



**十二. 二进制运算的应用**

题目分类	题目编号
异或的应用	89、136、137、260、268
与或非的应用	371、318、201



**十四. 数据结构**

题目分类	题目编号
数据结构设计——栈与队列	225、232、284、622、641、155
数据结构设计——哈希表	676、355、380、381
数据结构设计——哈希与双向链表	432、146、460
前缀树	208、211、648、386、677、472、421、212、336、440
堆	23、373、378、632、347、692、502、630、407、295、480
树状数组	307、315、493、327、673
线段树	699
平衡树(set/map)	352、218、363

**十五. 采样**

题目分类	题目编号
按权值采样	528、497
蓄水池抽样	382、398
拒绝采样	470、478、519

**十六. 计算几何**

题目分类	题目编号
计算几何基础	593、447、223、149
分类讨论法	335
凸包	587
覆盖问题	391

**十七. 常用技巧与算法**

题目分类	题目编号
博弈论	292
分块	239、164
倍增法	330
拓展欧几里得算法	365
洗牌算法	384
找规律	390、672
分治法	395、667
排序算法	147、148
线性筛	204
摩尔投票法	229



## **十三. 动态规划**


| **数组中的动态规划**           | **509、70、338、45、55、198、213、650、91、639、552、123、188、309、32、264、313、403** |
| ------------------------------ | :----------------------------------------------------------- |
| **子数组、子序列中的动态规划** | **689、413、446、368、416、279**                             |
| **背包问题**                   | **322、518、474、494、377**                                  |
| **矩阵中的动态规划**           | **62、63、64、120、576、688、221、629、174、96、329**        |
| **动态规划与字符串匹配**       | **583、72、97、115、516、132、131、139、140、514、10、44**   |
| **状态压缩动态规划**           | **464、691、698、638、473**                                  |
| **区间中的动态规划**           | **486、664、375、312、546**                                  |
| **树形dp**                     | **337、124**                                                 |
| **数位dp**                     | **233、600**                                                 |
|                                |                                                              |

### 数组中的动态规划

### [509. 斐波那契数](https://leetcode-cn.com/problems/fibonacci-number/)

**斐波那契数**，通常用 `F(n)` 表示，形成的序列称为 **斐波那契数列** 。该数列由 `0` 和 `1` 开始，后面的每一项数字都是前面两项数字的和。也就是：

```
F(0) = 0，F(1) = 1
F(n) = F(n - 1) + F(n - 2)，其中 n > 1
```

给你 `n` ，请计算 `F(n)` 。

**示例 1：**

```
输入：2
输出：1
解释：F(2) = F(1) + F(0) = 1 + 0 = 1
```

**示例 2：**

```
输入：3
输出：2
解释：F(3) = F(2) + F(1) = 1 + 1 = 2
```

```java
//动态规划 添加备忘录
class Solution {
    public int fib(int n) {
        if(n==0)return 0;
        if(n==1||n==2)return 1;
        int []memo = new int[n+1];
        memo[1] = 1;
        memo[2] = 1;
        for(int i=3;i<=n;i++){
            memo[i] = memo[i-1]+memo[i-2];
        }
        return memo[n];
    }
}
//优化空间 仅使用两个变量保存临时数据
class Solution {
    public int fib(int n) {
        if(n==0)return 0;
        if(n==1||n==2)return 1;
        int pre=1,cur=1;
        int tmp;
        for(int i=3;i<=n;i++){
            tmp = pre+cur;
            pre = cur;
            cur = tmp;
        }
        return cur;
    }
}
```

### [70. 爬楼梯](https://leetcode-cn.com/problems/climbing-stairs/)

假设你正在爬楼梯。需要 *n* 阶你才能到达楼顶。

每次你可以爬 1 或 2 个台阶。你有多少种不同的方法可以爬到楼顶呢？

**注意：**给定 *n* 是一个正整数。

**示例 1：**

```
输入： 2
输出： 2
解释： 有两种方法可以爬到楼顶。
1.  1 阶 + 1 阶
2.  2 阶
```

**示例 2：**

```
输入： 3
输出： 3
解释： 有三种方法可以爬到楼顶。
1.  1 阶 + 1 阶 + 1 阶
2.  1 阶 + 2 阶
3.  2 阶 + 1 阶
```

```java
//与上一题思路一样
class Solution {
    public int climbStairs(int n) {
        if(n==1)return 1;
        if(n==2)return 2;
        int pre = 1;
        int cur = 2;
        int tmp;
        for(int i=3;i<=n;i++){
            tmp = pre+cur;
            pre = cur;
            cur = tmp;
        }
        return cur;
    }
}
```

### [338. 比特位计数](https://leetcode-cn.com/problems/counting-bits/)

给定一个非负整数 **num**。对于 **0 ≤ i ≤ num** 范围中的每个数字 **i** ，计算其二进制数中的 1 的数目并将它们作为数组返回。

**示例 1:**

```
输入: 2
输出: [0,1,1]
```

**示例 2:**

```
输入: 5
输出: [0,1,1,2,1,2]
```

**进阶:**

- 给出时间复杂度为**O(n\*sizeof(integer))**的解答非常容易。但你可以在线性时间**O(n)**内用一趟扫描做到吗？
- 要求算法的空间复杂度为**O(n)**。
- 你能进一步完善解法吗？要求在C++或任何其他语言中不使用任何内置函数（如 C++ 中的 **__builtin_popcount**）来执行此操作。

```java
//笨蛋解法 复杂度为O(n*sizeof(Integer))
class Solution {
    public int[] countBits(int num) {
        if(num==0)return new int[]{0};
        int []res = new int [num+1];
        for(int i =0;i<num+1;i++){
            res[i] = comput(i);
        }
        return res;
    }
    public int comput(int num){//算每个数的二进制形式中1的个数
        int count = 0;
        while(num>0){
            count+=num%2;
            num/=2;
        }
        return count;
    }
}
//观察规律 动态规划 i为偶数：num[i]=num[i/2] ;i为奇数 num[i]=num[i/2]+1;
//添加位运算
class Solution {
    public int[] countBits(int num) {
        // 0  1  10  11 100 101 110 111 1000 1001   1010  1011  1100  1101
        // 0  1   2  3  4    5   6   7   8    9      10     11    12   13
        // 1110 1111  100000
        // 14   15    16
        int []res = new int [num+1];
        for(int i =1;i<=num;i++){
            // i / 2 is i >> 1 and i % 2 is i & 1
            res[i] = res[i>>1]+(i&1);
        }
        return res;
    }
}
```

### [55. 跳跃游戏](https://leetcode-cn.com/problems/jump-game/)

给定一个非负整数数组，你最初位于数组的第一个位置。

数组中的每个元素代表你在该位置可以跳跃的最大长度。

判断你是否能够到达最后一个位置。

**示例 1:**

```
输入: [2,3,1,1,4]
输出: true
解释: 我们可以先跳 1 步，从位置 0 到达 位置 1, 然后再从位置 1 跳 3 步到达最后一个位置。
```

**示例 2:**

```
输入: [3,2,1,0,4]
输出: false
解释: 无论怎样，你总会到达索引为 3 的位置。但该位置的最大跳跃长度是 0 ， 所以你永远不可能到达最后一个位置。
```

```java
//自己写的笨蛋解法 用到了递归和备忘录标记，若一趟操作确定为false则将其nums为置为0
class Solution {
    public boolean canJump(int[] nums) {
        if(nums.length==0)return false;
        return dp(nums,0);
}
    public boolean dp(int []nums,int cur){
        if(cur>=nums.length-1)return true;
        if(nums[cur]==0)return false;
        for(int i=nums[cur];i>=1;i--){
            if(dp(nums,cur+i)==true) return true;
            else{
                nums[cur+i] = 0;
            }
        }
        return false;
    }
}
//贪心算法 正向 1、reach用于标识目前能达到的最大距离，当reach>=length-1时说明可以到达
//2、另一关键点在于i<=reach用于判断当前位置i是否可以通过前面的元素跳跃至当前位置i
class Solution {
    public boolean canJump(int[] nums) {
        int reach = 0;
        int n = nums.length;
        for(int i=0;i<n;i++){
            if(i<=reach){
                reach = Math.max(reach,i+nums[i]);
                if(reach>=n-1)return true;
            }
        }
        return false;
    }
}
//另一版本，将reach的判断放在的最后，理论上用时会更多些，因为少了提前终止return true这一步，但代码更简洁了
class Solution {
    public boolean canJump(int[] nums) {
        int reach = 0;
        int n = nums.length;
        for(int i=0;i<n&&i<=reach;i++){
              reach = Math.max(reach,i+nums[i]);
        }
        return reach>=n-1;
    }
}
//贪心算法 反向 从最后一个位置开始，默认可达，向前推，若该位置i可达则将reach置为i表示前面的元素可以通过i到达数组尾部，直到数组开头若reach=0则可达，不等于0则不可达
class Solution {
    public boolean canJump(int[] nums) {
        int reach = nums.length-1;
        for(int i=reach-1;i>=0;i--){
            if(i+nums[i]>=reach){
                reach = i;
            }
        }
        return reach==0;
    }
}
```

### [45. 跳跃游戏 II](https://leetcode-cn.com/problems/jump-game-ii/)

给定一个非负整数数组，你最初位于数组的第一个位置。

数组中的每个元素代表你在该位置可以跳跃的最大长度。

你的目标是使用最少的跳跃次数到达数组的最后一个位置。

**示例:**

```
输入: [2,3,1,1,4]
输出: 2
解释: 跳到最后一个位置的最小跳跃数是 2。
     从下标为 0 跳到下标为 1 的位置，跳 1 步，然后跳 3 步到达数组的最后一个位置。
```

**说明:**

假设你总是可以到达数组的最后一个位置。

```JAVA
//方法一：反向查找出发位置
//自己写的笨比算法 时间复杂度很高 官方的笨比解法本质上和这个一样，结果还超时了
//从前往后依次找到一个距离reach最远且可达的点，然后将这个点设置为reach，
//从头再开始找一遍，直到reach=0标识找到了开头->循环结束，返回count
class Solution {
    public int jump(int[] nums) {
        int reach = nums.length-1;
        int count = 0;
        int i=0;
        while(i!=reach){
            if(nums[i]+i>=reach){
                reach = i;
                count+=1;
                i=0;
            }else{
                i++;
            }
        }
        return count;
    }
}
//方法二：正向查找 时间复杂度O(n)
//贪心算法 理解有难度，目前感觉理解了50%吧 
class Solution {
    public int jump(int[] nums) {
        int now_max_distance=0;
        int end=0;//边界，代表了每次跳跃中的最右位置，一旦i到达了边界，就需要更新新的边界，并count++
        int count = 0;
        int length = nums.length;
        for(int i=0;i<length-1;i++){
            now_max_distance = Math.max(now_max_distance,i+nums[i]);
            if(i==end){
                end = now_max_distance;
                count++;
            }
        }
        return count;
    }
}
//方法三 动态规划(超时)
//目前脑子不够用了
//需要多次遍历的方法，时间复杂度很高，leetcode超时
class Solution {
    public int jump(int[] nums) {
        int length = nums.length;
        int []dp = new int [length];
        dp[0] = 0;
        for(int i=1;i<length;i++){
            dp[i] = length+1;//初始化为一个很大的值
        }
        for(int i=0;i<length;i++){
            for(int j=0;j<i;j++){
                if(j+nums[j]>=i){
                    dp[i] = Math.min(dp[i],dp[j]+1);
                }
            }
        }
        return dp[length-1];
    }
}
//方法四 动态规划 优化版 不会超时
class Solution {
    public int jump(int[] nums) {
        int length = nums.length;
        int []dp = new int [length];
        dp[0] = 0;
        for(int i=1;i<length;i++){
            dp[i] = length+1;//初始化为一个很大的值
        }
        for(int i=0;i<length;i++){
            for(int j=1;j<=nums[i];j++){
                if(i+j>=length) {
                    return dp[length-1];
                }else{
                    dp[i+j] = Math.min(dp[i+j],dp[i]+1);
                }
            }
        }
        return dp[length-1];
    }
}
```

### [198. 打家劫舍](https://leetcode-cn.com/problems/house-robber/)

你是一个专业的小偷，计划偷窃沿街的房屋。每间房内都藏有一定的现金，影响你偷窃的唯一制约因素就是相邻的房屋装有相互连通的防盗系统，**如果两间相邻的房屋在同一晚上被小偷闯入，系统会自动报警**。

给定一个代表每个房屋存放金额的非负整数数组，计算你 **不触动警报装置的情况下** ，一夜之内能够偷窃到的最高金额。

**示例 1：**

```
输入：[1,2,3,1]
输出：4
解释：偷窃 1 号房屋 (金额 = 1) ，然后偷窃 3 号房屋 (金额 = 3)。
     偷窃到的最高金额 = 1 + 3 = 4 。
```

**示例 2：**

```
输入：[2,7,9,3,1]
输出：12
解释：偷窃 1 号房屋 (金额 = 2), 偷窃 3 号房屋 (金额 = 9)，接着偷窃 5 号房屋 (金额 = 1)。
     偷窃到的最高金额 = 2 + 9 + 1 = 12 。
```

**提示：**

- `0 <= nums.length <= 100`
- `0 <= nums[i] <= 400`

```java
//方法 动态规划 自己还是没想出来 不过也正常 一共没做几个题 代码是自己写的 还不错
//状态转移方程 dp[i] =max(dp[i-1],dp[i-2]+num[i])
class Solution {
    public int rob(int[] nums) {
        int length = nums.length;
        if(length==0)return 0;
        if(length==1)return nums[0];
        if(length==2)return Math.max(nums[0],nums[1]);
        int []dp = new int [length];
        dp[0] = nums[0];
        dp[1] = Math.max(dp[0],nums[1]);
        for(int i=2;i<length;i++){
            dp[i] = Math.max(dp[i-2]+nums[i],dp[i-1]);
        }
        return dp[length-1];
    }
}
//[1,2,3,1]  1+3=4
//[2,7,9,3,1] 2+9+1=12
//[1,3,6,8,2,5,3,1]  3+8+5+1=17
```

### [213. 打家劫舍 II](https://leetcode-cn.com/problems/house-robber-ii/)

你是一个专业的小偷，计划偷窃沿街的房屋，每间房内都藏有一定的现金。这个地方所有的房屋都 **围成一圈** ，这意味着第一个房屋和最后一个房屋是紧挨着的。同时，相邻的房屋装有相互连通的防盗系统，**如果两间相邻的房屋在同一晚上被小偷闯入，系统会自动报警** 。

给定一个代表每个房屋存放金额的非负整数数组，计算你 **在不触动警报装置的情况下** ，能够偷窃到的最高金额。

**示例 1：**

```
输入：nums = [2,3,2]
输出：3
解释：你不能先偷窃 1 号房屋（金额 = 2），然后偷窃 3 号房屋（金额 = 2）, 因为他们是相邻的。
```

**示例 2：**

```
输入：nums = [1,2,3,1]
输出：4
解释：你可以先偷窃 1 号房屋（金额 = 1），然后偷窃 3 号房屋（金额 = 3）。
     偷窃到的最高金额 = 1 + 3 = 4 。
```

**示例 3：**

```
输入：nums = [0]
输出：0
```

**提示：**

- `1 <= nums.length <= 100`
- `0 <= nums[i] <= 1000`

```java
//与上题的不同点在于首和尾元素最多只能取其一，因此开辟两个dp数组分别包含首和尾求dp，最后返回两者中大的哪一个
//我真棒~
class Solution {
    public int rob(int[] nums) {
        int length = nums.length;
        if(length==1)return nums[0];
        if(length==2)return Math.max(nums[0],nums[1]);
        int []dp1 = new int [length-1];
        int []dp2 = new int [length-1];
        dp1[0] = nums[0];
        dp1[1] = Math.max(dp1[0],nums[1]);
        for(int i=2;i<length-1;i++){
            dp1[i] = Math.max(dp1[i-2]+nums[i],dp1[i-1]);
        }
        dp2[0] = nums[1];
        dp2[1] = Math.max(dp2[0],nums[2]);
        for(int i=2;i<length-1;i++){
            dp2[i] = Math.max(dp2[i-2]+nums[i+1],dp2[i-1]);
        }
        return Math.max(dp1[length-2],dp2[length-2]);
    }
}
```

### [650. 只有两个键的键盘](https://leetcode-cn.com/problems/2-keys-keyboard/)

最初在一个记事本上只有一个字符 'A'。你每次可以对这个记事本进行两种操作：

1. `Copy All` (复制全部) : 你可以复制这个记事本中的所有字符(部分的复制是不允许的)。
2. `Paste` (粘贴) : 你可以粘贴你**上一次**复制的字符。

给定一个数字 `n` 。你需要使用最少的操作次数，在记事本中打印出**恰好** `n` 个 'A'。输出能够打印出 `n` 个 'A' 的最少操作次数。

**示例 1:**

```
输入: 3
输出: 3
解释:
最初, 我们只有一个字符 'A'。
第 1 步, 我们使用 Copy All 操作。
第 2 步, 我们使用 Paste 操作来获得 'AA'。
第 3 步, 我们使用 Paste 操作来获得 'AAA'。
```

**说明:**

1. `n` 的取值范围是 [1, 1000] 。

```java
//自己目前想到的动态规划解法，根据规律能得出dp[i]与i的最大可除整数的dp值有关即dp[i] = dp[maxnum] +i/maxnum    耗时多点
class Solution {
    public int minSteps(int n) {
        if(n==1)return 0;
        int []dp = new int [n+1];
        dp[1] = 0;
        for(int i=2;i<=n;i++){
            int maxnum = getmaxnum(i);
            dp[i] = dp[maxnum] + i/maxnum;
        }
        return dp[n];
    }
    public int getmaxnum(int n){
        for(int i=n/2;i>=0;i--){
            if(n%i==0){
                return i;
            }
        }
        return 0;
    }
}
//评论区的一种做法，和自己的解法本质上相同，但是巧妙的是没有用dp数组，因为求n所以不需要把前面所有的1->n-1都求出来，只需要求与n相关的那些数就可以了    耗时少了很多
class Solution {
    public int minSteps(int n) {
        if(n==1)return 0;
        int count=0;
        int dp = n;
        while(dp>1){
            int i = getmaxnum(dp);
            count+=dp/i;
            dp = i;
        }
        return count;
    }
    public int getmaxnum(int n){
        for(int i=n/2;i>=0;i--){
            if(n%i==0){
                return i;
            }
        }
        return 0;
    }
}
```

### [91. 解码方法](https://leetcode-cn.com/problems/decode-ways/)

一条包含字母 `A-Z` 的消息通过以下映射进行了 **编码** ：

```
'A' -> 1
'B' -> 2
...
'Z' -> 26
```

要 **解码** 已编码的消息，所有数字必须基于上述映射的方法，反向映射回字母（可能有多种方法）。例如，`"111"` 可以将 `"1"` 中的每个 `"1"` 映射为 `"A"` ，从而得到 `"AAA"` ，或者可以将 `"11"` 和 `"1"`（分别为 `"K"` 和 `"A"` ）映射为 `"KA"` 。注意，`"06"` 不能映射为 `"F"` ，因为 `"6"` 和 `"06"` 不同。

给你一个只含数字的 **非空** 字符串 `num` ，请计算并返回 **解码** 方法的 **总数** 。

题目数据保证答案肯定是一个 **32 位** 的整数。

**示例 1：**

```
输入：s = "12"
输出：2
解释：它可以解码为 "AB"（1 2）或者 "L"（12）。
```

**示例 2：**

```
输入：s = "226"
输出：3
解释：它可以解码为 "BZ" (2 26), "VF" (22 6), 或者 "BBF" (2 2 6) 。
```

**示例 3：**

```
输入：s = "0"
输出：0
解释：没有字符映射到以 0 开头的数字。含有 0 的有效映射是 'J' -> "10" 和 'T'-> "20" 。由于没有字符，因此没有有效的方法对此进行解码，因为所有数字都需要映射。
```

**示例 4：**

```
输入：s = "06"
输出：0
解释："06" 不能映射到 "F" ，因为字符串开头的 0 无法指向一个有效的字符。 
```

**提示：**

- `1 <= s.length <= 100`
- `s` 只包含数字，并且可能包含前导零。

```java
//动态规划，虽然写出来了 但是用的时间太长了而且逻辑很混乱 代码和思路可以再好好整改。
//ps:自己简化的最终版本 但是耗时很长
class Solution {
    public int numDecodings(String s) {
        int length = s.length();
        if(length==0||s.charAt(0)=='0')return 0;
        if(length==1)return 1;
        int []nums = new int[length];
        for(int i=0;i<length;i++){
            nums[i] = Integer.parseInt(s.charAt(i)+"");
        }
        int []dp = new int [length+1];
        dp[0] = dp[1] = 1;
        for(int i=2;i<=length;i++){
            if(judge(nums[i-2],nums[i-1])==true){
                if(nums[i-1]==0)dp[i] = dp[i-2];//1220
                else dp[i] = dp[i-1]+dp[i-2];//1221
            }else{
                if(nums[i-1]==0) dp[i] =0;//1230
                else dp[i] = dp[i-1];//1231
            }
        }
        return dp[length];
    }
    public boolean judge(int a,int b){
        if(a==1||(a==2&&b<=6))return true;
        return false;
    }
}
```

### [639. 解码方法 2](https://leetcode-cn.com/problems/decode-ways-ii/)

一条包含字母 `A-Z` 的消息通过以下的方式进行了编码：

```
'A' -> 1
'B' -> 2
...
'Z' -> 26
```

除了上述的条件以外，现在加密字符串可以包含字符 '*'了，字符'*'可以被当做1到9当中的任意一个数字。

给定一条包含数字和字符'*'的加密信息，请确定解码方法的总数。

同时，由于结果值可能会相当的大，所以你应当对109 + 7取模。（翻译者标注：此处取模主要是为了防止溢出）

**示例 1 :**

```
输入: "*"
输出: 9
解释: 加密的信息可以被解密为: "A", "B", "C", "D", "E", "F", "G", "H", "I".
```

**示例 2 :**

```
输入: "1*"
输出: 9 + 9 = 18（翻译者标注：这里1*可以分解为1,* 或者当做1*来处理，所以结果是9+9=18）
```

**说明 :**

1. 输入的字符串长度范围是 [1, 105]。
2. 输入的字符串只会包含字符 '*' 和 数字'0' - '9'. 

```java
//动态规划，傻逼解法 面向测试用例编程 这个题他妈的边界条件太多了日
class Solution {
    public int numDecodings(String s) {
        int M = 1000000007;
        int length = s.length();
        if(length==0||s.charAt(0)=='0')return 0;
        if(length==1)return s.charAt(0)=='*'? 9:1;
        long []dp = new long [length+1];
        if(s.charAt(0)=='*')dp[0]=dp[1] = 9;
        else dp[0]=dp[1] = 1;
        for(int i=2;i<=length;i++){
            if(s.charAt(i-1)=='*'){
                if(s.charAt(i-2)=='1')dp[i] = (dp[i-1]+dp[i-2])* 9 % M;
                else if(s.charAt(i-2)=='2')dp[i] = (dp[i-2]*6+dp[i-1]*9)%M;
                else if(s.charAt(i-2)=='*'){
                    if(i==2) dp[i] = (dp[i-1]*9+15*1)%M;
                    else dp[i] = (dp[i-1]*9+dp[i-2]*15)%M;
                }
                else dp[i] = (dp[i-1]*9)%M;
            }else{
                    if(judge(s.charAt(i-2),s.charAt(i-1))==true){
                    if(s.charAt(i-2)=='*'){
                        if(i==2){
                            if(s.charAt(i-1)=='0') dp[i] =2;
                            else if(s.charAt(i-1)<='6')dp[i] = (dp[i-1]+2)%M;
                                else dp[i] = (dp[i-1]+1)%M;
                        }else{
                            if(s.charAt(i-1)=='0')dp[i] =2*dp[i-2];
                            else if(s.charAt(i-1)<='6'&&s.charAt(i-1)>'0')dp[i] = (dp[i-1]+2*dp[i-2])%M;
                                else dp[i] = (dp[i-1]+1*dp[i-2])%M;
                        }
                        
                    }else{
                         if(s.charAt(i-1)=='0')dp[i] = dp[i-2];
                             else dp[i] = (dp[i-1]+dp[i-2])%M;
                    }
                }else{
                    if(s.charAt(i-1)=='0') dp[i] =0;
                        else dp[i] = dp[i-1];
                }
            }
        }
        return (int)dp[length];
    }
    public boolean judge(char a,char b){
        if(a=='*'||a=='1'||(a=='2'&&b<='6'))return true;
        return false;
    }
}
```

### [551. 学生出勤记录 I](https://leetcode-cn.com/problems/student-attendance-record-i/)

难度简单66

给定一个字符串来代表一个学生的出勤记录，这个记录仅包含以下三个字符：

1. **'A'** : Absent，缺勤
2. **'L'** : Late，迟到
3. **'P'** : Present，到场

如果一个学生的出勤记录中不**超过一个'A'(缺勤)**并且**不超过两个连续的'L'(迟到)**,那么这个学生会被奖赏。

你需要根据这个学生的出勤记录判断他是否会被奖赏。

**示例 1:**

```
输入: "PPALLP"
输出: True
```

**示例 2:**

```
输入: "PPALLL"
输出: False
```

```java
class Solution {
    public boolean checkRecord(String s) {
        int count1 = 0;
        int count2 = 0;
        for(int i=0;i<s.length();i++){
            if(s.charAt(i)=='A'){
                count1++;
                count2=0;
                if(count1>=2)break;
            }else if(s.charAt(i)=='L'){
                count2++;
                if(count2>=3)break;
            }else {
                count2=0;
            }
        }
        return count1>=2||count2>=3? false:true;
    }
}
```

### [552. 学生出勤记录 II](https://leetcode-cn.com/problems/student-attendance-record-ii/)

难度困难120

给定一个正整数 **n**，返回长度为 n 的所有可被视为可奖励的出勤记录的数量。 答案可能非常大，你只需返回结果mod 109 + 7的值。

学生出勤记录是只包含以下三个字符的字符串：

1. **'A'** : Absent，缺勤
2. **'L'** : Late，迟到
3. **'P'** : Present，到场

如果记录不包含**多于一个'A'（缺勤）**或**超过两个连续的'L'（迟到）**，则该记录被视为可奖励的。

**示例 1:**

```
输入: n = 2
输出: 8 
解释：
有8个长度为2的记录将被视为可奖励：
"PP" , "AP", "PA", "LP", "PL", "AL", "LA", "LL"
只有"AA"不会被视为可奖励，因为缺勤次数超过一次。
```

```java
class Solution {
    public int checkRecord(int n) {
        int _MOD = 1000000007;
        long [][][]dp = new long [n+1][2][3];
        dp[1][0][0] = 1;
        dp[1][0][1] = 1;
        dp[1][1][0] = 1;
        for(int i =2;i<=n;i++){
            dp[i][0][0] = (dp[i-1][0][0]+dp[i-1][0][1]+dp[i-1][0][2])%_MOD;
            dp[i][0][1] = dp[i-1][0][0];
            dp[i][0][2] = dp[i-1][0][1];
            dp[i][1][0] = (dp[i-1][1][0]+dp[i-1][1][1]+dp[i-1][1][2])%_MOD;
            dp[i][1][0]+=(dp[i-1][0][0]+dp[i-1][0][1]+dp[i-1][0][2])%_MOD;
            dp[i][1][1] = dp[i-1][1][0];
            dp[i][1][2] = dp[i-1][1][1];
        }
        return (int) ((dp[n][0][0] + dp[n][0][1] + dp[n][0][2] + dp[n][1][0] + dp[n][1][1] + dp[n][1][2]) % _MOD);
    }
}

// 压缩状态空间
class Solution {
    public int checkRecord(int n) {
        int _MOD = 1000000007;
        long dp00,dp01,dp02,dp10,dp11,dp12;
        dp00 = dp01 = dp10 = 1;
        dp11 = dp12 = dp02 = 0;
        for(int i =2;i<=n;i++){
            long t00 = dp00, t01 = dp01, t02 = dp02, t10 = dp10, t11 = dp11, t12 = dp12;
            dp00 = (t00+t01+t02)%_MOD;
            dp01 = t00;
            dp02 = t01;
            dp10 = (t00+t01+t02)%_MOD;
            dp10+=(t10+t11+t12)%_MOD;
            dp11 = t10;
            dp12 = t11;
        }
    return (int)((dp00+dp01+dp02+dp10+dp11+dp12)%_MOD);
    }
}
```

### 01背包问题

```JAVA
import java.util.*;


public class Solution {
    /**
     * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
     * 计算01背包问题的结果
     * @param V int整型 背包的体积
     * @param n int整型 物品的个数
     * @param vw int整型二维数组 第一维度为n,第二维度为2的二维数组,vw[i][0],vw[i][1]分别描述i+1个物品的vi,wi
     * @return int整型
     */
    public int knapsack (int V, int n, int[][] vw) {
       if(V==0 || n==0 || vw==null){
            return 0;
        }
        int[][] dp=new int[n+1][V+1];
        for(int i=1;i<=n;i++){
            for(int j=1;j<=V;j++){
                if(j<vw[i-1][0]){
                    dp[i][j]=dp[i-1][j];
                }
                else{
                    dp[i][j]=Math.max(dp[i-1][j],dp[i-1][j-vw[i-1][0]]+vw[i-1][1]);
                }
            }
        }
        return dp[n][V];
    }
}
```

## 十四、Leetcode刷题

### [146. LRU 缓存机制](https://leetcode-cn.com/problems/lru-cache/)

```JAVA
class LRUCache {
    int size;
    int capacity;
    DLinkedList head,tail;
    Map<Integer,DLinkedList>cache = new HashMap<>();
    class DLinkedList{
        DLinkedList prev;
        DLinkedList next;
        int key;
        int value;
        public DLinkedList(){}
        public DLinkedList(int key,int value){
            this.key = key;
            this.value = value;
        }
    }
    public LRUCache(int capacity) {
        size =0;
        this.capacity = capacity;
        head = new DLinkedList();
        tail = new DLinkedList();
        head.next =tail;
        tail.prev = head;
    }
    
    public int get(int key) {
        DLinkedList node = cache.get(key);
        if(node==null)return -1;
        else{
            movetoHead(node);
            return node.value;
        }
    }
    
    public void put(int key, int value) {
        DLinkedList node = cache.get(key);
        if(node==null){
            DLinkedList newNode = new DLinkedList(key,value);
            cache.put(key,newNode);
            addtoHead(newNode);
            size++;
            if(size>capacity){
                DLinkedList tail =  removeTail();
                size--;
                cache.remove(tail.key);
            }
        }else{
            node.value = value;
            movetoHead(node);
        }
    }

    public void addtoHead(DLinkedList node){
        node.prev = head;
        node.next = head.next;
        head.next.prev = node;
        head.next = node;
    }
    public void movetoHead(DLinkedList node){
        removeNode(node);
        addtoHead(node);
        
    }
    public void removeNode(DLinkedList node){
        node.prev.next = node.next;
        node.next.prev = node.prev;
    }
    public DLinkedList removeTail(){
        DLinkedList node = tail.prev;
        removeNode(node);
        return node;
    }
}

/**
 * Your LRUCache object will be instantiated and called as such:
 * LRUCache obj = new LRUCache(capacity);
 * int param_1 = obj.get(key);
 * obj.put(key,value);
 */
```

