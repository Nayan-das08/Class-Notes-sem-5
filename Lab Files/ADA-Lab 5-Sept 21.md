%%[[_Lab Files]]%%
%%#lab/ada%%
# Experiment 5
Sept 21, 2022

## Objective
Implement Greedy Algorithms for Fractional Knapsack Problem and Task Scheduling Problem.

## Resources
C

## Program Logic / Algorithm
### Fractional Knapsack Problem
```plain
frac_knapsack(array v, array w, int W)
{
	1. for i <- i to size(v)
		2. do P[i] <- v[i] / w[i]
	3. sort_desc(P)
	4. set i <- 1
	5. while W > 0
		6. do amount <- min(W, w[i])
		7. solution[i] <- amount
		8. set W <- W - amount
		9. set i <- i+1
	10. return solution[]
}
```

### Task Scheduling
```plain
Task_sch(array deadline, array penalty)
{
	1. sort_desc(penalty)
	2. set m <- max(deadline)
	3. set m <- size(deadline)
	4. let scheduled[1:m], not_scheduled[1:(n-m)]
	5. for i <- 1 to n
		6. for j <- deadline[i] to 1, by -1
			7. if schedule[j-1] slot is empty
				8. do schedule[j-1] = task[i]
		9. if task not scheduled
			10. do not_scheduled[k] = task[i]
	11. return scheduled[], not_scheduled[]
}
```

## Source Code
### Code for Fractional Knapsack Problem
```plain
# include <stdio.h>
# include <stdlib.h>
# include <time.h>

int n;

struct item
{
	int weight, value, P;
};

int min(int a, int b)
{
	if (a<b)
		return a;
	else
		return b;
}

void swap(struct item arr[], int i, int j)
{
	struct item temp = arr[i];
	arr[i] = arr[j];
	arr[j] = temp;
}

int partition(struct item arr[], int p, int r)
{
	int pivot = arr[r].P; // setting last element as pivot
	int i=p;
	for (int j=p; j<r; j++)
		if (arr[j].P >= pivot)
			swap(arr, i++, j);
	swap(arr, i, r); 
	return i;
}

void quick(struct item arr[], int p, int r)
{
	int q;
	if (p < r)
	{
		q = partition(arr, p, r);
		quick(arr, p, q-1);
		quick(arr, q+1, r);
	}
}

float Greedy(struct item I[], int W)
{
	// getting profit per unit weight into I[i].P
	for (int i=0; i<n; i++)
		I[i].P = I[i].value / I[i].weight;

	// sort
	quick(I,0,n-1);
	
	// show Items
	printf("List of items :-\n\n");
	printf("    \tWEIGHT \tVALUE \tPROFIT\n");
	for (int i=0; i<n; i++)
		printf("%d \t%d \t%d \t%d\n", i, I[i].weight, I[i].value, I[i].P);
	
	// --------------------------------------------------------

	int 	amount = 0;		// amount to be put in knapsack
	int 	j;				// index variable
	int 	profit;		    // profit for each insertion into the knapsack
	int 	*knapsack = (int *) calloc(n,sizeof(int));
	float 	total_profit = 0;

	printf("\n\n");
	printf("Items put in knapsack :-\n\n");
	printf("    \tI.WT \tMIN \tI.VAL \tPROFIT \tREM\n");

	j=0;
	while (W > 0 && j < n)
	{
		// get min value among item weight and remaining weight
		// if (item weight < remaining weight): put item in knapsack
			// profit is the value of the item

		// if (remaining weight < item weight): put remaining weight's worth of item in knapsack
			// profit is (remaining weight) / (item weight) * (item value)
		amount = min(I[j].weight, W);

		//put amount in knapsack
		knapsack[j] = amount;

		// update the knapsack weight value
		W -= amount;

		// general profit
		profit = ((float)amount / I[j].weight )*I[j].value;
		printf("%d \t%d \t%d \t%d \t%d \t%d\n",j , I[j].weight, amount, I[j].value, profit, W);
		j++;
		total_profit += profit;
	}

	free(knapsack);
	return total_profit;
}

int main(int argc, char *argv[])
{
	int W=10; 
	float total_profit;
	char choice;
	
	printf("Enter weight of knapsack : ");
	scanf("%d", &W);
	printf("Enter number of items    : ");
	scanf("%d", &n);	
	
	struct item *I = (struct item*) calloc(n,sizeof(struct item));
	
	for (int i=0; i<n; i++)
	{
		printf("\nitem %d:\n", i);
		printf("  weight : ");
		scanf("%d", &I[i].weight);
		printf("  value  : ");
		scanf("%d", &I[i].value);
	}

	printf("Capacity of knapsack : %d\n", W);
	printf("Number of items      : %d\n\n", n);
	
	total_profit = Greedy(I,W);
	printf("\n\nTotal Profit = %.2f",total_profit);

	free(I);
	return 0;
}
```

### Code for Task Scheduling Problem
```plain
# include <stdio.h>
# include <stdlib.h>

struct task
{
	int id, d, p;
};

int n;

// quick sort
void swap(struct task arr[], int i, int j)
{
	struct task temp = arr[i];
	arr[i] = arr[j];
	arr[j] = temp;
}

int partition(struct task arr[], int p, int r)
{
	int pivot = arr[r].p; // setting last element as pivot
	int i=p;
	for (int j=p; j<r; j++)
		if (arr[j].p >= pivot)
			swap(arr, i++, j);
	swap(arr, i, r); 
	return i;
}

void quick(struct task arr[], int p, int r)
{
	int q;
	if (p < r)
	{
		q = partition(arr, p, r);
		quick(arr, p, q-1);
		quick(arr, q+1, r);
	}
}

int get_max_deadline(struct task tasks[])
{
	int max = 0;
	for (int i=0; i<n; i++)
	{
		if (tasks[i].d > max)
			max = tasks[i].d;
	}
	return max;
}

int main()
{
	printf("Enter number of tasks : ");
	scanf("%d", &n);
	struct task *tasks = (struct task *) calloc(n,sizeof(struct task));

	for (int i=0; i<n; i++)
	{
		printf("\nTask %d:\n", i+1);
		tasks[i].id = i+1;
		printf("  deadline : ");
		scanf("%d", &tasks[i].d);
		printf("  penalty  : ");
		scanf("%d", &tasks[i].p);
	}
	// printf("")

	quick(tasks,0,n-1);

	printf("\n\nID\tDeadline\tProfit\n");
	for (int i=0; i<n; i++)
		printf("%2d\t  %2d\t\t  %2d\n", tasks[i].id, tasks[i].d, tasks[i].p);

	int m = get_max_deadline(tasks);
	struct task *scheduled = (struct task *) calloc(m,sizeof(struct task));
	struct task *not_scheduled = (struct task *) calloc(n-m,sizeof(struct task));
	int d, flag;

	printf("\n");
	int k=0;
	for (int i=0; i<n; i++)
	{
		d = tasks[i].d;
		flag=0;
		for (int j=d; (j-1)>=0; j--)
		{
			if (scheduled[j-1].id == 0)
			{
				scheduled[j-1] = tasks[i];
				flag=1;
				break;
			}
		}
		if (flag == 0)
		{
			not_scheduled[k++] = tasks[i];
		}
	}

	printf("\nscheduled : \n");
	
	for (int i=0; i<m; i++)
		printf("+-----");
	printf("+\n");

	for (int i=0; i<m; i++)
		printf("|  %d  ", scheduled[i].id);
	printf("|\n");

	for (int i=0; i<m; i++)
		printf("+-----");
	printf("+\n");

	for (int i=0; i<=m; i++)
		printf("%d     ", i);
	
	
	int penalty = 0;
	printf("\n\nnot scheduled : ");
	for (int i=0; i<(n-m); i++)
	{
		printf("%d  ", not_scheduled[i].id);
		penalty += not_scheduled[i].p;
	}

	int profit = 0;
	for (int i=0; i<m; i++)
	{
		profit += scheduled[i].p;
	}

	printf("\n\nPenalty = %d", penalty);
	// printf("\n\nProfit = %d", profit);

	return 0;
}
```


## Output
### Fractional Knapsack Problem Output
```plain
Enter weight of knapsack : 60
Enter number of items    : 5

item 0:
  weight : 5
  value  : 30

item 1:
  weight : 10
  value  : 20

item 2:
  weight : 20
  value  : 100

item 3:
  weight : 30
  value  : 90

item 4:
  weight : 40
  value  : 160
Capacity of knapsack : 60
Number of items      : 5

List of items :-

        WEIGHT  VALUE   PROFIT
0       5       30      6
1       20      100     5
2       40      160     4
3       30      90      3
4       10      20      2


Items put in knapsack :-

        I.WT    MIN     I.VAL   PROFIT  REM
0       5       5       30      30      55
1       20      20      100     100     35
2       40      35      160     140     0


Total Profit = 270.00
```

### Task Scheduling Problem Output
```plain
Enter number of tasks : 7

Task 1:
  deadline : 4
  penalty  : 70

Task 2:
  deadline : 2
  penalty  : 60

Task 3:
  deadline : 5
  penalty  : 50

Task 4:
  deadline : 3
  penalty  : 40

Task 5:
  deadline : 1
  penalty  : 30

Task 6:
  deadline : 4
  penalty  : 20

Task 7:
  deadline : 6
  penalty  : 10


ID      Deadline        Profit
 1         4              70
 2         2              60
 3         5              50
 4         3              40
 5         1              30
 6         4              20
 7         6              10


scheduled :
+-----+-----+-----+-----+-----+-----+
|  5  |  2  |  4  |  1  |  3  |  7  |
+-----+-----+-----+-----+-----+-----+
0     1     2     3     4     5     6

not scheduled : 6

Penalty = 20
```

## Analysis
The Fractional Knapsack Problem can be solved optimally using the Greedy Approach to solve an optimization problem. As per the methodology, we sort the items in decreasing order of their per unit profits. This helps in selecting the items which can give the maximum profit for their respective weights. If the knapsack can not fit an entire item we fill the knapsack with a fraction of the item, thus dividing the value of the item as well.

Since sorting the list of items is the most computationally expensive task, the time complexity depends completely on the algorithm used for sorting. 