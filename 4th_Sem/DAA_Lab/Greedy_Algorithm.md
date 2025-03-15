# Greedy Algorithm
*    ### Fractional Knapsack Problem &emsp; &emsp;&emsp; &emsp; &emsp;[method 1](#fractional-knapsack-problem-method-1) &emsp; [method 2](#fractional-knapsack-problem-method-2)
*    ### Job Scheduling with Deadline Problem &emsp; [method 1](#job-scheduling-with-deadline-problem-method-1) &emsp; [method 2](#job-scheduling-with-deadline-problem-method-2)
<br>  

### Fractional Knapsack Problem Method 1
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
} Block;

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
    printf("Enter total number of Blocks(maximum: %d): ", SIZE_LIMIT);
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
### Fractional Knapsack Problem Method 2

```C
/* write a C program to implement Fractional Knapsack problem using Greedy approach */
/*Last updated : 15-03-2025*/

#include <stdio.h>
#include <stdlib.h>
#define SIZE_LIMIT 7

typedef struct block {
    int no;
    int check;
    float weight;
    float profit;
    float profit_per_unit;
} Block;

void display(Block arr[], int size) {
    int i;
    printf("\nNo   Profit \t Weight    Profit_per_Unit\n");
    for (i = 0; i < size; i++) {
        printf(" %d    %.2f \t %.2f \t\t %.2f\n", arr[i].no, arr[i].profit, arr[i].weight, arr[i].profit_per_unit);
    }
}

int main() {
    Block arr[SIZE_LIMIT], temp;
    int i, j, size, indx, max0;
    float capacity, avalible, total_profit = 0;
    printf("Enter total number of Blocks(maximum: %d):", SIZE_LIMIT);
    scanf("%d", &size);
    for (i = 0; i < size; i++) { //taking input data
        arr[i].no = i;
        arr[i].check = 0;
        printf("Enter Weight value of Block %d: ", i);
        scanf("%f", &arr[i].weight);
        printf("Enter Profit value of Block %d: ", i);
        scanf("%f", &arr[i].profit);
        arr[i].profit_per_unit = arr[i].profit / arr[i].weight;
    }
    printf("\nBlocks Data as per input");
    display(arr, size);

    printf("\nEnter Load Capacity Value: ");
    scanf("%f", &capacity);
    avalible = capacity;

    while (avalible > 0) {
        indx = -1;
        for (i = 0; i < size; i++) { // find best unused block
            if (arr[i].check == 0) { // filter unused block
                if ((indx == -1) || (arr[i].profit_per_unit > max0)) {
                    indx = i;
                    max0 = arr[i].profit_per_unit;
                }
            }
        }
        arr[indx].check = 1;
        printf("\nChoose Block %d, here profit per unit= %.2f ", arr[indx].no, arr[indx].profit_per_unit);
        if (avalible >= arr[indx].weight) { // when enough space avalible take a full block 
            printf("take full part");
            total_profit += arr[indx].profit;
            avalible -= arr[indx].weight;
        }
        else { // when enough spacce not avalible take a block by parttiion
            printf("take %.2f part", avalible / arr[indx].weight);
            total_profit += avalible * arr[indx].profit_per_unit;
            avalible = 0;
        }
        printf("\n\t Now profit = %.2f and Remaining Capacity = %.2f", total_profit, avalible);
    }

    printf("\n\nFor Capacity %.2f, Total Profit will be %.2f", capacity, total_profit);

    return 0;
}

/*
Enter total number of Blocks(maximum: 7):7
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

Blocks Data as per input
No   Profit      Weight    Profit_per_Unit
 0    10.00      2.00            5.00
 1    5.00       3.00            1.67
 2    15.00      5.00            3.00
 3    7.00       7.00            1.00
 4    6.00       1.00            6.00
 5    18.00      4.00            4.50
 6    3.00       1.00            3.00

Enter Load Capacity Value: 15

Choose Block 4, here profit per unit= 6.00 take full part
         Now profit = 6.00 and Remaining Capacity = 14.00
Choose Block 0, here profit per unit= 5.00 take full part
         Now profit = 16.00 and Remaining Capacity = 12.00
Choose Block 5, here profit per unit= 4.50 take full part
         Now profit = 34.00 and Remaining Capacity = 8.00
Choose Block 2, here profit per unit= 3.00 take full part
         Now profit = 49.00 and Remaining Capacity = 3.00
Choose Block 6, here profit per unit= 3.00 take full part
         Now profit = 52.00 and Remaining Capacity = 2.00
Choose Block 1, here profit per unit= 1.67 take 0.67 part
         Now profit = 55.33 and Remaining Capacity = 0.00

For Capacity 15.00, Total Profit will be 55.33

*/
```
## Job Scheduling with Deadline Problem method 1
```C
/* write a C program to implement Job Scheduling with Deadline problem using Greedy approach */
/*Last updated : 15-03-2025*/

#include <stdio.h>
#include <stdlib.h>
#define SIZE_LIMIT 7

typedef struct job {
    int no;
    float profit;
    int deadline;
} Job;

void display(Job arr[], int size) {
    int i;
    printf("\nNo   Profit \t Deadline\n");
    for (i = 0; i < size; i++) {
        printf(" %d    %.2f  \t\t %d\n", arr[i].no, arr[i].profit, arr[i].deadline);
    }
}

int main() {
    Job arr[SIZE_LIMIT], temp;
    int i, j, size, slot_seq[SIZE_LIMIT], time_limit, time_slot, c;
    float total_profit = 0;
    printf("Enter total number of Job(maximum: %d): ", SIZE_LIMIT);
    scanf("%d", &size);
    for (i = 0; i < size; i++) { //taking input data
        arr[i].no = i;
        printf("Enter Profit value of job %d  : ", i);
        scanf("%f", &arr[i].profit);
        printf("Enter Deadline value of job %d: ", i);
        scanf("%d", &arr[i].deadline);
        slot_seq[i] = -1;
    }

    printf("\nEnter Maximum Deadline Value: ");
    scanf("%d", &time_limit);

    for (i = 0; i < size - 1; i++) { // Sorting blocks based on profit per unit
        for (j = 0; j < size - 1 - i; j++) {
            if (arr[j].profit < arr[j + 1].profit) {
                temp = arr[j];
                arr[j] = arr[j + 1];
                arr[j + 1] = temp;
            }
        }
    }
    printf("\nJobs Data after sorting based on profit");
    display(arr, size);

    for (i = 0; i < size; i++) {
        if (arr[i].deadline > time_limit) {
            time_slot = time_limit - 1;
        }
        else {
            time_slot = arr[i].deadline - 1;
        }
        /* find a free slot starting from the last of the job's deadline to the beginning of timeline */
        while (time_slot >= 0 && slot_seq[time_slot] != -1) {
            time_slot--;
        }
        /* if a free slot is found, insert the job to the slot array at time_slot index
        else the job is not added to the schedule */
        if (time_slot >= 0 && slot_seq[time_slot] == -1) {
            slot_seq[time_slot] = arr[i].no;
            total_profit += arr[i].profit;
            printf("\nChoose job:%d, place at index:%d after Iteration:%d: Profit will be = %.2f", arr[i].no, time_slot, i, total_profit);
        }
        else {
            printf("\nChoose job:%d, possible slot not Avalible, Job discarded ",arr[i].no);
        }
        printf("\nCurrent Job Sequence no: ");
        for (j = 0; j < time_limit; j++) {
            printf("%d ", slot_seq[j]);
        }
    }
    c = 0;
    /* check whether a intermediate Slot is unallocated or not 
       if found fill this slot with next allocated job slot*/
    for (i = 0; i < time_limit; i++) {
        if (slot_seq[i] == -1) { // 
            printf("\ni=%d time_limit=%d", i, time_limit);
            c++;
            slot_seq[i] = slot_seq[i + c];
        }
    }
    printf("\nFinal profit=%.2f for Slot order Sequence: ", total_profit);
    for (j = 0; j < time_limit; j++) {
        printf("job:%d  ", slot_seq[j]);
    }

    return 0;
}

/*
Enter total number of Job(maximum: 7): 4
Enter Profit value of job 0  : 20
Enter Deadline value of job 0: 4
Enter Profit value of job 1  : 25
Enter Deadline value of job 1: 1
Enter Profit value of job 2  : 30
Enter Deadline value of job 2: 2
Enter Profit value of job 3  : 40
Enter Deadline value of job 3: 2

Enter Maximum Deadline Value: 3

Jobs Data after sorting based on profit
No   Profit      Deadline
 3    40.00              2
 2    30.00              2
 1    25.00              1
 0    20.00              4

Choose job:3, place at index:1 after Iteration:0: Profit will be = 40.00
Current Job Sequence no: -1 3 -1 
Choose job:2, place at index:0 after Iteration:1: Profit will be = 70.00
Current Job Sequence no: 2 3 -1 
Choose job:1, possible slot not Avalible, Job discarded 
Current Job Sequence no: 2 3 -1 
Choose job:0, place at index:2 after Iteration:3: Profit will be = 90.00
Current Job Sequence no: 2 3 0 
Final profit=90.00 for Slot order Sequence: job:2  job:3  job:0  

*/
```

### Job Scheduling with Deadline Problem method 2
