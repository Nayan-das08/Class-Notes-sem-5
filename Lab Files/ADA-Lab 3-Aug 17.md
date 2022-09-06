%%[[_Lab Files]]%%
%%#lab/ada%%
# Experiment 
Aug 17, 2022

## Objective


## Resources
C

## Program Logic / Algorithm
### Merge Sort
```plain
Put algo here
```

### Quick Sort
```plain
QuickSort(array[], p, r)
{
	if p < r, then:
		1. set q = partition(array, p, r)
		2. QuickSort(array, p, q-1)
		3. QuickSort(array, q+1, r)
}

Partition(array[], p, q, r)
{
	1. pivot = array[r]
	2. set i = p
	3. Repeat for j=p to r
		1. if 
	
}
```

## Pseudo-code
```plain
// merge and quick sort

# include <stdio.h>
# include <stdlib.h>
# include <time.h>
# include <ctype.h>

const int size = 10;

void swap(int arr[], int i, int j)
{
	int temp = arr[i]; 
	arr[i] = arr[j];
	arr[j] = temp;
}

void merge(int arr[], int start, int m, int end, int *step)
{
	int n1 = (m+1)-start;
	int n2 = end-(m);

	// get two arrays
	int a[n1], b[n2];
	for (int i=0; i<n1; i++)
		a[i] = arr[start+i];
	for (int i=0; i<n2; i++)
		b[i] = arr[m+1+i];

	// merge sort
	int i=0, j=0, k=start; 
	while (i < n1 && j < n2)
	{
		(*step)++;
		if (a[i] < b[j])
			arr[k++] = a[i++];
		else
			arr[k++] = b[j++];
	}
	while (i < n1)
	{
		(*step)++;
		arr[k++] = a[i++];
	}
	while (j < n2)
	{
		(*step)++;
		arr[k++] = b[j++];	
	}
}

void mergeSort(int arr[], int start, int end, int *step)
{
	int m;
	if (start < end) 
	// some element exists in arr[start] to arr[end]
	{
		m = (start + end)/2;
		mergeSort(arr, start, m, step);
		mergeSort(arr, m+1, end, step);
		merge(arr, start, m, end, step);
		for (int i=0; i<size; i++)
			printf("%2d  ", arr[i]);
		printf("\n");
	}	
}

int partition(int arr[], int p, int r, int *step)
{
	(*step)++;
	int pivot = arr[r]; // setting last element as pivot
	int i=p;
	for (int j=p; j<r; j++)
		if (arr[j] <= pivot)
			swap(arr, i++, j);
	swap(arr, i, r); 

	for (int i=0; i<size; i++)
		printf("%d  ", arr[i]);
	printf("\n");

	return i;
}

void quickSort(int arr[], int p, int r, int *step)
{
	int q;
	if (p < r) 
	// elements exist in array
	{
		q = partition(arr, p, r, step);
		quickSort(arr, p, q-1, step);
		quickSort(arr, q+1, r, step);
	}
}

int main()
{
	int arr[size], step, choice;
	char y_n;

	do
	{
		// get array
		srand(time(0)+rand());
		for (int i=0; i<size; i++)
			arr[i] = rand()%100;

		printf("\nChoose from the following :-\n");
		printf("    1. Merge Sort \n    2. Quick Sort");
		printf("\n\n    Enter choice : ");
		scanf("%d", &choice);

		step = 0;

		switch (choice)
		{
			case 1:
			{
				printf("\nMERGE SORT\n");
				
				// before
				for (int i=0; i<size; i++)
					printf("%2d  ", arr[i]);
				printf("\n\n");
				
				mergeSort(arr, 0, size-1, &step);
				
				// after
				printf("\n");
				for (int i=0; i<size; i++)
					printf("%2d  ", arr[i]);
				printf("\n\nsteps taken = %d", step);
			}
			break;

			case 2:
			{
				printf("\nQUICK SORT\n");

				// before
				for (int i=0; i<size; i++)
					printf("%2d  ", arr[i]);
				printf("\n\n");
				
				quickSort(arr, 0, size-1, &step);
				
				// after
				printf("\n");
				for (int i=0; i<size; i++)
					printf("%2d  ", arr[i]);
				printf("\n\nsteps taken = %d", step);
			}
			break;

			default: printf("\nINVALID INPUT OF CHOICE");
		}
		printf("\n\nDo you wish to continue? (y/n) : ");
		scanf("%s", &y_n);
	}
	while('y' == tolower(y_n));
	printf("\nexited program");

	return 0;
}

```

## Output
```plain
Choose from the following :-
    1. Merge Sort
    2. Quick Sort

    Enter choice : 1

MERGE SORT
72  62  58   8   5   8  76  75  27  40

62  72  58   8   5   8  76  75  27  40
58  62  72   8   5   8  76  75  27  40
58  62  72   5   8   8  76  75  27  40
 5   8  58  62  72   8  76  75  27  40
 5   8  58  62  72   8  76  75  27  40
 5   8  58  62  72   8  75  76  27  40
 5   8  58  62  72   8  75  76  27  40
 5   8  58  62  72   8  27  40  75  76
 5   8   8  27  40  58  62  72  75  76

 5   8   8  27  40  58  62  72  75  76

steps taken = 34

Do you wish to continue? (y/n) : y

Choose from the following :-
    1. Merge Sort
    2. Quick Sort

    Enter choice : 2

QUICK SORT
71  11  94   6   9  48  22  44   4  15

11  6  9  4  15  48  22  44  71  94
4  6  9  11  15  48  22  44  71  94
4  6  9  11  15  48  22  44  71  94
4  6  9  11  15  48  22  44  71  94
4  6  9  11  15  48  22  44  71  94
4  6  9  11  15  48  22  44  71  94
4  6  9  11  15  22  44  48  71  94

 4   6   9  11  15  22  44  48  71  94

steps taken = 7

Do you wish to continue? (y/n) : n

exited program
```

## Analysis
