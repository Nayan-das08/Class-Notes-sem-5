%%[[_Lab Files]]%%
%%#lab/ada%% 
# Experiment 10
Nov 2, 2022

## Objective
Implement N-Queen Problem using Backtracking

## Resources
C

## Program Logic / Algorithm
```plain
N-Queen(n)
{
	1. Initialize the array a[1..n] to 0.
	2. Set k to 1.
	3. While k is not 0 do the following:
	    4. Set a[k] to a[k] + 1.
	    5. If a[k] is greater than n, then set k to k - 1.
	    3. Otherwise, if a[k] does not conflict with 
	       any of the queens already on the board, 
	       then set k to k + 1.
	    7. Otherwise, if a[k] does conflict with one 
	       or more of the queens already on the board, 
	       then go back to step 3a.
	    8. If k is equal to n + 1, then a solution 
	       has been found and you can print it out.
	       Then set k to k - 1.
}
```

## Source Code
```plain
#include <stdio.h>
#include <stdlib.h>
#include<math.h>
#include<conio.h>

int *a, count=0;

int place(int pos)
{
    int i;
    for(i=1; i<pos; i++)
    {
        if((a[i]==a[pos])||((abs(a[i]-a[pos])==abs(i-pos))))
            return 0;
    }
    return 1;
}

void print_sol(int n)
{
    int i, j;
    count++;
    if(n <= 6)
    {
        printf("\n\nSolution %d:\n", count);
        for(i=1; i<=n; i++)
        {
            printf("    ");
            for (int k=1; k<=n; k++)
                printf("+---");
            printf("+\n    ");

            for(j=1; j<=n; j++)
            {
                printf("|");
                if(a[i] == j)
                    printf(" Q ");
                else
                    printf(" * ");
            }
            printf("|\n");
        }
        printf("    ");
        for (int k=1; k<=n; k++)
            printf("+---");
        printf("+\n");   
    }
}

void queen(int n)
{
    int k=1;
    a = (int *)malloc(n*sizeof(int));
    a[k] = 0;
    while(k != 0)
    {
        a[k] = a[k]+1;
        while((a[k]<=n) && !place(k))
            a[k]++;

        if(a[k] <= n)
        {
            if(k == n)
                print_sol(n);
            else
            {
                k++;
                a[k] = 0;
            }
        }
        else
            k--;
    }
}


int main()
{
    printf("N-QUEEN PROBLEM\n(Backtracking)\n\n");
    int n;
    printf("Enter the number of queens: ");
    scanf("%d", &n);
    queen(n);
    printf("\n\nTotal solutions: %d", count);
    return 0;
}
```

## Output
```plain
N-QUEEN PROBLEM
(using Backtracking)

Enter the number of queens: 4


Solution 1:
    +---+---+---+---+
    | * | Q | * | * |
    +---+---+---+---+
    | * | * | * | Q |
    +---+---+---+---+
    | Q | * | * | * |
    +---+---+---+---+
    | * | * | Q | * |
    +---+---+---+---+


Solution 2:
    +---+---+---+---+
    | * | * | Q | * |
    +---+---+---+---+
    | Q | * | * | * |
    +---+---+---+---+
    | * | * | * | Q |
    +---+---+---+---+
    | * | Q | * | * |
    +---+---+---+---+


Total solutions: 2
```

## Analysis
First queen will have $n$ placements, second must not be in same column, and must be oblique to the first so $(n-1)$ possibilities and so on, hence worst case time complexity $O(n!)$. 