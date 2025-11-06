# Two sum

question - https://leetcode.com/problems/two-sum/description/

Algorithm - 
1. Maintain a dictionary storing ech numbers as key and value 
2. loop throught the list given
3. get the compliment = target - list[i]
4. check if compliment exist in dictionary - if exists return the indices
5. add the looping number inside the hash map

```c#

public class Solution {
    public int[] TwoSum(int[] nums, int target) {
        Dictionary<int, int> map = new Dictionary<int, int>();

        for(int i=0;i<nums.Length;i++){
            int compliment = target - nums[i];
            if(map.ContainsKey(compliment)){
                return new int[] {map[compliment], i};
            }
            map[nums[i]] = i;
        }

        return new int[] {};
    }
}
```