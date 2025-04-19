# Divide and Conquer Approach
*    ### Find Maximum and Minimum element from an Array &emsp; &emsp;&emsp; &emsp; &emsp;[method 1](#find-maximum-and-minimum-element-from-an-array)
*    ### Minimum number of Scalar Multiplications needed for Chain of Matrix &emsp; [method 1](#minimum-number-of-scalar-multiplications-needed-for-chain-of-matrix)
<br>  


### Find Maximum and Minimum element from an Array
```C
/* write a C program to Find Maximum and Minimum element from an Array using Divide and Conquer Approach */
/*Last updated : 19-04-2025*/
#include <stdio.h>
#include <stdlib.h>
#define SIZE 10

/* Define a structure to hold both minimum and maximum values. */
typedef struct minmax {
    int min;
    int max;
}
MinMax;

/* A recursive function that finds minimum and maximum in the subarray arr[low...high] */
MinMax findMinMax(int arr[], int low, int high) {
    MinMax result, leftResult, rightResult;

    // Base case: Only one element
    if (low == high) {
        result.min = arr[low];
        result.max = arr[low];
        return result;
    }

    /* Base case: If there are two elements, compare them directly */
    if (high == low + 1) {
        if (arr[low] < arr[high]) {
            result.min = arr[low];
            result.max = arr[high];
        } else {
            result.min = arr[high];
            result.max = arr[low];
        }
        return result;
    }

    /* recursive case: if there are more than two value,
    we divide the array into two part and recursivelly call each part  */
    /* Divide the array into two halves  */
    int mid = (low + high) / 2;
    leftResult = findMinMax(arr, low, mid);
    rightResult = findMinMax(arr, mid + 1, high);

    /* Combine the results of the two halves (Conquer step for Min)  */
    if (leftResult.min < rightResult.min) {
        result.min = leftResult.min;
    }
    else {
        result.min = rightResult.min;
    }

    /* Combine the results of the two halves (Conquer step for Max)  */
    if (leftResult.max > rightResult.max) {
        result.max = leftResult.max;
    }
    else {
        result.max = rightResult.max;
    }

    return result;
}

int main() {

    int arr[SIZE], n, i;
    printf("Enter Size of the Array(not more than %d): ", SIZE);
    scanf("%d", &n);
    for (i = 0; i < n; i++) {
        printf("Enter number for index %d: ",i);
        scanf("%d", &arr[i]);
    }

    /* Get minimum and maximum using our divide and conquer function */
    MinMax result = findMinMax(arr, 0, n - 1);

    // Display the results
    printf("\nMinimum element is %d", result.min);
    printf("\nMaximum element is %d", result.max);

    return 0;
}

/* OUTPUT :-
Enter Size of the Array(not more than 10): 10
Enter number for index 0: 34
Enter number for index 1: 67
Enter number for index 2: 23
Enter number for index 3: 89
Enter number for index 4: 12
Enter number for index 5: 45
Enter number for index 6: 78
Enter number for index 7: 56
Enter number for index 8: 90
Enter number for index 9: 31

Minimum element is 12
Maximum element is 90

*/

```

### Minimum number of Scalar Multiplications needed for Chain of Matrix

```C
#include <stdio.h>
#include <limits.h>
#define SIZE 5
// Recursive function to compute the minimum cost of multiplying matrices
// from index i to j given the dimensions in array p.
// Note: For a chain of n matrices, p[] has n+1 elements.
// The matrix chain is:
//    Matrix A1: p[0] x p[1]
//    Matrix A2: p[1] x p[2]
//    ...
//    Matrix An: p[n-1] x p[n]
int matrixChainMultiplication(int p[], int i, int j) {
    // Base case: When there is only one matrix,
    // no multiplications are needed.
    if (i == j)
        return 0;

    int k;
    int minCost = INT_MAX;
    int count;

    // Partition the matrix chain at every possible split point
    // and calculate the minimum cost.
    for (k = i; k < j; k++) {
        count = matrixChainMultiplication(p, i, k)
              + matrixChainMultiplication(p, k + 1, j)
              + p[i - 1] * p[k] * p[j];  // Cost of multiplying the two parts

        if (count < minCost)
            minCost = count;
    }
    return minCost;
}

int main() {
    // Example:
    // Consider 4 matrices with dimensions:
    // A1: 40x20, A2: 20x30, A3: 30x10, A4: 10x30
    // The dimensions array will then be {40, 20, 30, 10, 30}
    int arr[SIZE], n, i,result;
    printf("Enter Size of the Array(not more than %d): ", SIZE);
    scanf("%d", &n);
    printf("Enter row number for matrix 1: ");
    scanf("%d", &arr[0]);
    for (i = 1; i < n; i++) {
        printf("Enter column number for index %d: ",i);
        scanf("%d", &arr[i]);
    }

    result = matrixChainMultiplication(arr, 1, n - 1);
    printf("Minimum number of multiplications is %d\n", result);

    return 0;
}

/* OUTPUT :-
Enter Size of the Array(not more than 5): 5
Enter row number for matrix 1: 4
Enter column number for index 1: 2
Enter column number for index 2: 3
Enter column number for index 3: 1
Enter column number for index 4: 3
Minimum number of multiplications is 26

```
