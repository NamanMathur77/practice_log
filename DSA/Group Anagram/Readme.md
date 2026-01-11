question - https://leetcode.com/problems/group-anagrams/
```C#
public class Solution {
    public IList<IList<string>> GroupAnagrams(string[] strs) {
        var map = new Dictionary<string, List<string>>();

        foreach(string s in strs){
            int[] count = new int[26];
            foreach(c in s){
                count[c-'a']++;
            }

            string key = string.Join('#', count);

            if(!map.ContainsKey(key)){
                map[key] = new List<string>();
            }
            map[key].add(s);
        }
        return map.Values.Cast<IList<string>>().ToList();
    }
}
```
