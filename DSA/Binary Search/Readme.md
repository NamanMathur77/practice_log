https://leetcode.com/problems/binary-search/

```C#
public class Solution {
    public int Search(int[] nums, int target) {
        int i=0;
        int j = nums.Length-1;
        while(i<=j){
            if(nums[i]==target){
                return i;
            }
            if(nums[j]==target){
                return j;
            }
            if(nums[j]>target){
                j-=1;
            }
            if(nums[i]<target){
                i+=1;
            }
        }

        return -1;

    }
}
```