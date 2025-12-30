https://leetcode.com/problems/car-fleet/description/

## Algorithm
1. Arrange the cars in ascending order with their position.
2. from backwards loop through the cars and calculate when they are going to achieve teh target.
3. push the target in the stack.
4. If the length of stack is greater than 2 check top two times if lower one is going to finish earlier then the current pushing one then pop the stack
5. the length of the stack is the number of car fleets there are.

```C#
public class Solution {
    public int CarFleet(int target, int[] position, int[] speed) {
        int n = position.Length;
        if (n == 0) return 0;

        // Build list of (position, time_to_target)
        var cars = new (int pos, double time)[n];
        for (int i = 0; i < n; i++) {
            double t = (double)(target - position[i]) / speed[i];
            cars[i] = (position[i], t);
        }

        Array.Sort(cars, (a, b) => b.pos.CompareTo(a.pos));

        Stack<double> stack = new Stack<double>();

        foreach (var car in cars)
        {
            // If current car takes longer than the fleet ahead,
            // it forms a new fleet
            if (stack.Count == 0 || car.time > stack.Peek())
            {
                stack.Push(car.time);
            }
            // else: car joins the fleet ahead → do nothing
        }
        return stack.Count;
    }
}
```