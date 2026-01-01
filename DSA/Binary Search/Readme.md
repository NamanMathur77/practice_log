https://leetcode.com/problems/binary-search/

```C#
public class Solution {
    public int Search(int[] nums, int target) {
        int i=0;
        int j = nums.Length-1;
        while(i<=j){
            int mean = (i+j)/2;
            if(nums[mean]>target){
                j = mean-1;
            }
            else if(nums[mean]<target){
                i = mean+1;
            }
            else{
                return mean;
            }
        }
        return -1;
    }
}
```