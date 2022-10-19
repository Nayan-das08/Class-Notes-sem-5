%%[[_Lab Files]]%%
%%#lab/ada%%
%%#incomplete%% 
# Experiment 6
Oct 5, 2022

## Objective
Implement Dynamic Programming for solving Global Knapsack Problem.

## Resources
C

## Program Logic / Algorithm
```plain
knapsack(M, items)
{
	1. for w = 0 to M
		2. c[0,w] = 0
	3. for i = 1 to n
		4. c[i,0] = 0
		5. for w = 1 to M
			6. if items[i].w <= w and 
			   items[i].v + c[i-1,w-items[i].w]
				7. c[i,w] = items[i].v + c[i-1,w-items[i].w]
				8. keep[i,w] = 1
			9. else
				10. c[i,w] = c[i-1,w]
				11. keep[i,w] = 0
	12. k = M
	13. for i = n to 1, by -1
		14. if keep[i,k] == 1
			15. print i
			16. k = k - items[i].w
}
```

## Source Code
```plain
# include <stdio.h>
# include <stdlib.h>

int n, W;

// void show(int **arr, int n, int W)
void show(int arr[n][W], char mat_name)
{
	printf("%c  | ", mat_name);
	for (int i=0; i<W; i++)
		printf("%3d  ", i);
	printf("\n---");
	for (int i=0; i<W; i++)
		printf("-----");
	printf("\n");
	
	for (int i=0; i<n; i++)
	{
		printf("%d  | ", i);
		for (int j=0; j<W; j++)
			printf("%3d  ", arr[i][j]);
		printf("\n");
	}	
	printf("\n\n");
}

int max(int a, int b)
{
	if (a > b)
		return a;
	else
		return b;
}

int main()
{
	// int w[] = {0,3,2,4,1};
	// int v[] = {0,100,20,60,40};
	int w[] = {0,1,2,5,6,7};
	int v[] = {0,1,6,18,22,28};
	// int n, W;
	// n = 4+1;
	// W = 7+1;
	n = 5+1;
	W = 10+1;

	printf("\t  W    V\n");
	printf("------------------\n");
	for (int i=1; i<n; i++)
	{
		printf("item_%d    %d    %d\n", i, w[i], v[i]);
	}
	printf("\n\n");

	int C[n][W], keep[n][W];

	for (int i=0; i<n; i++)
		for (int j=0; j<W; j++)
			if (i == 0 || j == 0)
			{
				C[i][j] = 0;
				keep[i][j] = 0;
			}
			else
			{
				C[i][j] = -1;
				keep[i][j] = -1;	
			}

/*	for (int i=1; i<n; i++)
	{
		for (int j=1; j<W; j++)
		{
			if (w[i] > j)
			{
				C[i][j] = C[i-1][j];
				keep[i][j] = 0;
			}
			else if (w[i] <= j)
			{
				C[i][j] = max(C[i-1][j], v[i]+C[i-1][j-w[i]]);
				keep[i][j] = 1;
			}
		}
	}
*/	
	for (int i=1; i<n; i++)	
	{
		for (int j=1; j<W; j++)
		{
			if ((w[i] <= j) && ((v[i] + C[i-1][j-w[i]]) > C[i-1][j]))
			{
				C[i][j] = v[i] + C[i-1][j-w[i]];
				keep[i][j] = 1;
			}
			else
			{
				C[i][j] = C[i-1][j];
				keep[i][j] = 0;
			}
		}
	}

	show(C, 'C');
	show(keep, 'K');

	int total_profit = 0;
	printf("Items put in knapsack :-\n");
	int k = W-1; 
	for (int i=n-1; i>=1; i--)
	{
		if (keep[i][k] == 1)
		{
			printf("    item_%d, \tweight = %d, \tvalue = %d\n", i, w[i], v[i]);
			k = k - w[i];
			total_profit += v[i];
		}
	}
	printf("\n\nTotal Profit = %d", total_profit);
}
```

## Output
```plain
          W    V
------------------
item_1    1    1
item_2    2    6
item_3    5    18
item_4    6    22
item_5    7    28


C  |   0    1    2    3    4    5    6    7    8    9   10
----------------------------------------------------------
0  |   0    0    0    0    0    0    0    0    0    0    0
1  |   0    1    1    1    1    1    1    1    1    1    1
2  |   0    1    6    7    7    7    7    7    7    7    7
3  |   0    1    6    7    7   18   19   24   25   25   25
4  |   0    1    6    7    7   18   22   24   28   29   29
5  |   0    1    6    7    7   18   22   28   29   34   35


K  |   0    1    2    3    4    5    6    7    8    9   10
----------------------------------------------------------
0  |   0    0    0    0    0    0    0    0    0    0    0
1  |   0    1    1    1    1    1    1    1    1    1    1
2  |   0    0    1    1    1    1    1    1    1    1    1
3  |   0    0    0    0    0    1    1    1    1    1    1
4  |   0    0    0    0    0    0    1    0    1    1    1
5  |   0    0    0    0    0    0    0    1    1    1    1


Items put in knapsack :-
    item_5,     weight = 7,     value = 28
    item_2,     weight = 2,     value = 6
    item_1,     weight = 1,     value = 1


Total Profit = 35
```

## Analysis
