```C#
public class Solution {
    public int MaxArea(int[] height) {
        int max_area = 0;
        int i = 0;
        int j = height.Length-1;
        while(i<j){
            int area = (j-i)*(Math.Min(height[i], height[j]));
            max_area = Math.Max(area, max_area);
            if(height[i]>height[j]){
                j-=1;
            }
            else{
                i+=1;
            }
        }
        return max_area;
    }
}
```