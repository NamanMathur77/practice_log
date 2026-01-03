https://leetcode.com/problems/koko-eating-bananas/description/

```C#
public class Solution {
    public int MinEatingSpeed(int[] piles, int h) {

        int left = 1;
        int right = piles.Max();

        while(left<right){
            int mid = (left + right)/2;
            //find the time required to eat all piles
            int localTime = 0;
            foreach(int pile in piles){
                //one pile time
                int time = (pile+mid-1)/mid;
                //add pile time to the total time
                localTime +=time;
            }
            if(localTime>h){
                left = mid+1;
            }
            else{
                right = mid;
            }
        }
        return left;
        
    }
}
```