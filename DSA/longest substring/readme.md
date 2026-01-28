```C#
public int LengthOfLongestSubstring(string s) {
    int i = 0, j = 0, res = 0;
    HashSet<char> visited = new HashSet<char>();

    while (j < s.Length) {
        if (!visited.Contains(s[j])) {
            visited.Add(s[j]);
            res = Math.Max(res, j - i + 1);
            j++;
        } else {
            visited.Remove(s[i]);
            i++;
        }
    }

    return res;
}
```