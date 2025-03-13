```C
/* write a C program to implement Fractional Knapsack problem */

#include <stdio.h>
#include <stdlib.h>
#define SIZE 7

typedef struct block {
    int no;
    float weight;
    float profit;
    float profit_per_kg;
}
Block;

void display(Block arr[]) {
    int i;
    printf("\nNo   Profit \t Weight    Profit/weight\n");
    for (i = 0; i < SIZE; i++) {
        printf(" %d    %.2f \t %.2f \t\t %.2f\n", arr[i].no, arr[i].profit,
                        arr[i].weight, arr[i].profit_per_kg);
    }
}

int main() {
    Block arr[SIZE], temp;
    int i, j;
    float capacity, avalible, total_profit = 0;
    printf("Here Total number of Blocks is %d \n", SIZE);
    for (i = 0; i < SIZE; i++) {
        arr[i].no = i;
        printf("Enter Weight value of Block %d: ", i);
        scanf("%f", & arr[i].weight);
        printf("Enter Profit value of Block %d: ", i);
        scanf("%f", & arr[i].profit);
        arr[i].profit_per_kg = arr[i].profit / arr[i].weight;
    }

    printf("\nEnter Load Capacity Value: ");
    scanf("%f", & capacity);
    avalible = capacity;

    for (i = 0; i < SIZE - 1; i++) {
        for (j = 0; j < SIZE - 1 - i; j++) {
            if (arr[j].profit_per_kg < arr[j + 1].profit_per_kg) {
                temp = arr[j];
                arr[j] = arr[j + 1];
                arr[j + 1] = temp;
            }
        }
    }
    display(arr);

    for (i = 0; i < SIZE; i++) {
        if (avalible >= arr[i].weight) {
            printf("\nIteration %d: Choose Block %d, take full part here profit per kg= %.2f", i,
                            arr[i].no, arr[i].profit_per_kg);
            total_profit += arr[i].profit;
            avalible -= arr[i].weight;
            printf("\n\t Now profit = %.2f and Remaining Capacity = %.2f", total_profit, avalible);
        }
        else {
            printf("\nIteration %d: Choose Block %d, take %.2f part here profit per kg= %.2f", i, arr[i].no, 
                        avalible / arr[i].weight, arr[i].profit_per_kg);
            total_profit += avalible * arr[i].profit_per_kg;
            avalible = 0;
            printf("\n\t Now profit = %.2f and Remaining Capacity = %.2f", total_profit, avalible);
            break;
        }
    }

    printf("\n\nFor Capacity %.2f, Total Profit will be %.2f", capacity, total_profit);

    return 0;
}

/*
OUTPUT :-

Here Total number of Blocks is 7 
Enter Weight value of Block 0: 2
Enter Profit value of Block 0: 10
Enter Weight value of Block 1: 3
Enter Profit value of Block 1: 5
Enter Weight value of Block 2: 5
Enter Profit value of Block 2: 15
Enter Weight value of Block 3: 7
Enter Profit value of Block 3: 7
Enter Weight value of Block 4: 1
Enter Profit value of Block 4: 6
Enter Weight value of Block 5: 4
Enter Profit value of Block 5: 18
Enter Weight value of Block 6: 1
Enter Profit value of Block 6: 3

Enter Load Capacity Value: 15

No   Profit      Weight    Profit/weight
 4    6.00       1.00            6.00
 0    10.00      2.00            5.00
 5    18.00      4.00            4.50
 2    15.00      5.00            3.00
 6    3.00       1.00            3.00
 1    5.00       3.00            1.67
 3    7.00       7.00            1.00

Iteration 0: Choose Block 4, take full part here profit per kg= 6.00
         Now profit = 6.00 and Remaining Capacity = 14.00
Iteration 1: Choose Block 0, take full part here profit per kg= 5.00
         Now profit = 16.00 and Remaining Capacity = 12.00
Iteration 2: Choose Block 5, take full part here profit per kg= 4.50
         Now profit = 34.00 and Remaining Capacity = 8.00
Iteration 3: Choose Block 2, take full part here profit per kg= 3.00
         Now profit = 49.00 and Remaining Capacity = 3.00
Iteration 4: Choose Block 6, take full part here profit per kg= 3.00
         Now profit = 52.00 and Remaining Capacity = 2.00
Iteration 5: Choose Block 1, take 0.67 part here profit per kg= 1.67
         Now profit = 55.33 and Remaining Capacity = 0.00

For Capacity 15.00, Total Profit will be 55.33
*/
```
