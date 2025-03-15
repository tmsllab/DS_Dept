```C
/* write a C program to implement Fractional Knapsack problem using Greedy approach */
/*Last updated : 15-03-2025*/

#include <stdio.h>
#include <stdlib.h>
#define SIZE_LIMIT 7

typedef struct block {
    int no;
    float weight;
    float profit;
    float profit_per_unit;
}
Block;

void display(Block arr[],int size) {
    int i;
    printf("\nNo   Profit \t Weight    Profit_per_Unit\n");
    for (i = 0; i < size; i++) {
        printf(" %d    %.2f \t %.2f \t\t %.2f\n", arr[i].no, arr[i].profit,
                    arr[i].weight, arr[i].profit_per_unit);
    }
}

int main() {
    Block arr[SIZE_LIMIT], temp;
    int i, j,size;
    float capacity, avalible, total_profit = 0;
    printf("Enter total number of Blocks(maximum: %d): \n", SIZE_LIMIT);
    scanf("%d",&size);
    for (i = 0; i < size; i++) {  //taking input data
        arr[i].no = i;
        printf("Enter Weight value of Block %d: ", i);
        scanf("%f", &arr[i].weight);
        printf("Enter Profit value of Block %d: ", i);
        scanf("%f", &arr[i].profit);
        arr[i].profit_per_unit = arr[i].profit / arr[i].weight;
    }

    printf("\nEnter Load Capacity Value: ");
    scanf("%f", &capacity);
    avalible = capacity;

    for (i = 0; i < size - 1; i++) {  // Sorting blocks based on profit per unit
        for (j = 0; j < size - 1 - i; j++) {
            if (arr[j].profit_per_unit < arr[j + 1].profit_per_unit) {
                temp = arr[j];
                arr[j] = arr[j + 1];
                arr[j + 1] = temp;
            }
        }
    }
    printf("\nBlocks Data after sorting based on profit per unit");
    display(arr,size);

    for (i = 0; i < size; i++) {
        if (avalible >= arr[i].weight) {  // when enough space avalible take a full block 
            printf("\nIteration %d: Choose Block %d, take full part here profit per unit= %.2f", i,
                        arr[i].no, arr[i].profit_per_unit);
            
            total_profit += arr[i].profit;
            avalible -= arr[i].weight;
            
            printf("\n\t Now profit = %.2f and Remaining Capacity = %.2f", total_profit, avalible);
        }
        else {   // when enough spacce not avalible take a block by parttiion
            printf("\nIteration %d: Choose Block %d, take %.2f part here profit per unit= %.2f", i,
                        arr[i].no, avalible / arr[i].weight, arr[i].profit_per_unit);
            
            total_profit += avalible * arr[i].profit_per_unit;
            avalible = 0;
            
            printf("\n\t Now profit = %.2f and Remaining Capacity = %.2f", total_profit, avalible);
            break;
        }
    }

    printf("\n\nFor Capacity %.2f, Total Profit will be %.2f", capacity, total_profit);

    return 0;
}

/*
Enter total number of Blocks(maximum: 7): 7
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

Blocks Data after sorting based on profit per unit
No   Profit      Weight    Profit_per_Unit
 4    6.00       1.00            6.00
 0    10.00      2.00            5.00
 5    18.00      4.00            4.50
 2    15.00      5.00            3.00
 6    3.00       1.00            3.00
 1    5.00       3.00            1.67
 3    7.00       7.00            1.00

Iteration 0: Choose Block 4, take full part here profit per unit= 6.00
         Now profit = 6.00 and Remaining Capacity = 14.00
Iteration 1: Choose Block 0, take full part here profit per unit= 5.00
         Now profit = 16.00 and Remaining Capacity = 12.00
Iteration 2: Choose Block 5, take full part here profit per unit= 4.50
         Now profit = 34.00 and Remaining Capacity = 8.00
Iteration 3: Choose Block 2, take full part here profit per unit= 3.00
         Now profit = 49.00 and Remaining Capacity = 3.00
Iteration 4: Choose Block 6, take full part here profit per unit= 3.00
         Now profit = 52.00 and Remaining Capacity = 2.00
Iteration 5: Choose Block 1, take 0.67 part here profit per unit= 1.67
         Now profit = 55.33 and Remaining Capacity = 0.00

For Capacity 15.00, Total Profit will be 55.33

*/
```
