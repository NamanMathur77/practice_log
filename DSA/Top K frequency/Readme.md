question - https://leetcode.com/problems/top-k-frequent-elements/
```C#
public class Solution {
    public int[] TopKFrequent(int[] nums, int k) {
        Dictionary<int, int> freq = new Dictionary<int, int>();
        foreach(var num in nums){
            if(freq.ContainsKey(num)){
                freq[num]+=1;
            }
            else{
                freq[num]=1;
            }
        }

        var buckets = new List<int>[nums.Length+1];
        foreach(var kv in freq){
            int val = kv.Value;
            int key = kv.Key;
            if(buckets[val] == null){
                buckets[val]=new List<int>();
            }
            buckets[val].Add(key).
        }

        List<int> res = new List<int>();
        for(int i = buckets.Length - 1; i>=0 && res.Count<k; i--){
            if(buckets!=null){
                foreach(var num in buckets[i]){
                    res.Add(buckets[i]);
                    if(res.Count==k){
                        break;
                    }
                }
            }
        }
    }
}
```