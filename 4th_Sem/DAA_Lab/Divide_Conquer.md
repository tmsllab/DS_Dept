# Divide and Conquer Approach
*    ### Find Maximum and Minimum element from an Array &emsp; &emsp;&emsp; &emsp; &emsp;[method 1](#)
*    ### Job Scheduling with Deadline Problem &emsp; [method 1](#job-scheduling-with-deadline-problem-method-1) &emsp; [method 2](#job-scheduling-with-deadline-problem-method-2)
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

