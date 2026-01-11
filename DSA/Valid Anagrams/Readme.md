Question - https://leetcode.com/problems/valid-anagram/
```C#
public class Solution {
    public bool IsAnagram(string s, string t) {
        Dictionary<char, int> charsCount = new Dictionary<char, int>();
        if(s.Length != t. Length){
            return false;
        }

        foreach(char c in s){
            if(charsCount.ContainsKey(c)){
                charsCount[c]++;
            }
            else{
                charsCount[c]=1;
            }
        }

        foreach(char c in t){
            if(charsCount.ContainsKey(c)){
                charsCount[c] -=1;
                if(charsCount[c]<0){
                    return false;
                }
            }
            else{
                return false;
            }
        }
        return true;
    }
}
```