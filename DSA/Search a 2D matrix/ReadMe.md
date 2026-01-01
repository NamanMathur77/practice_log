https://leetcode.com/problems/search-a-2d-matrix/description/

```C#
public class Solution {
    public bool SearchMatrix(int[][] matrix, int target) {
        //find the number of rows and columns in the matrix given
        int rows = matrix.Length;
        int columns = matrix[0].Length;

        //find the row 
        int low = 0;
        int high = rows-1;
        int row = -1;
        while(low<=high){
            int mid = (low+high)/2;

            if(matrix[mid][0]<=target && matrix[mid][columns-1] >= target){
                row = mid;
                break;
            }
            else if(matrix[mid][0]>target){
                high = mid - 1;
            }
            else{
                low = mid + 1;
            }
        }

        if(row == -1){
            return false;
        }

        //find the number in this row
        int left = 0;
        int right = columns-1;

        while(left<=right){
            int mid = (left + right)/2;
            if(matrix[row][mid]>target){
                right = mid-1;
            }
            else if(matrix[row][mid]<target){
                left = mid+1;
            }
            else{
                return true;
            }
        }

        return false;

    }
}
```