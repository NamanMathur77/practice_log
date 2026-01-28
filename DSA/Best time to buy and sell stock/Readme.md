```C#
public class Solution {
    public int MaxProfit(int[] prices) {
        int maxProfit = 0;
        int buy = 0;

        for (int sell = 1; sell < prices.Length; sell++)
        {
            if (prices[sell] < prices[buy])
            {
                buy = sell;
            }
            else
            {
                maxProfit = Math.Max(maxProfit, prices[sell] - prices[buy]);
            }
        }

        return maxProfit;
    }
}
```