```C#
public class Solution {
    public int FindMin(int[] nums) {
        int i = 0;
        int j = nums.Length - 1;

        while (i < j) {
            int mid = i + (j - i) / 2;

            if (nums[mid] < nums[j]) {
                // Minimum is in left part including mid
                j = mid;
            } else {
                // Minimum is in right part excluding mid
                i = mid + 1;
            }
        }

        return nums[i];
    }
}
```