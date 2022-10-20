# Mock 02 | 19/10/2022 | Ionut_02 vs Lorenzo La Corte

## Exercise description

Given an m x n matrix and a target value, determine the location of the target value in the matrix. If the target value is not found in the matrix, print [Target Value] not found in the matrix.

Every row and column is sorted in increasing order in the given matrix.

### Links & material
* [Search in a row-wise and column-wise sorted matrix](https://www.educative.io/answers/how-to-search-in-a-row-wise-and-column-wise-sorted-matrix)


## Interview solution

```py
def searchMatrix(matrix, num : int):
	row1 = matrix[0]
  rowIndex = len(row)-1
  colIndex = 1

  for idx, elem in enumerate(row1):
  	if elem == num:
    	return True
    elif elem > num:
    	rowIndex = idx

	while(True):
  	if num == matrix[rowIndex][colIndex]:
    	return True
    else:
    	rowIndex -= 1

```

## Official solutions

```java
import java.util.Scanner;

public class Main {

    private static int[] search(int[][] matrix, int target) {
        if (matrix.length == 0) {  // If there are no elements in the matrix return -1
            return new int[]{-1, -1};
        }

        int numRows = matrix.length;
        int numCols = matrix[0].length;

        int i = 0; // Loop invariable for the row
        int j = numCols - 1; // Loop invariable for the column

        while (i >= 0 && i < numRows && j >= 0 && j < numCols) {
            if (target == matrix[i][j])  return new int[]{i, j};
            else if (target < matrix[i][j])  j--;
            else i++;
        }

        return new int[]{-1, -1};
    }

    public static void main(String[] args) {
        int[][] matrix = {
                {35,45,55,65},
                {40,50,60,70},
                {52,54,62,73},
                {57,58,64,75}
        };

        Scanner scanner = new Scanner(System.in);
        int target = scanner.nextInt();

        int[] result = search(matrix, target);

        if(result[0] != -1 && result[1] != -1) {
            System.out.println(target + " found at row - " + (result[0] + 1) + " and column - " + (result[1] + 1));
        } else {
            System.out.println(target + " not found in the matrix");
        }
    }
}
```
