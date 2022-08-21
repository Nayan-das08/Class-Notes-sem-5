%%[[_Lab Files]]%%
%%#lab/ada%% 
# Experiment 2
July 27, 2022

## Objective
Implement selection and bubble sort on an array of fixed size

## Resources
C

## Program Logic / Algorithm
```plain
SelectionSort(array[], size)
{
	1. Repeat for i=0 to size-1
		2. set small as i
			3. Repeat for j=1+i to size
				4. if array[j] is smaller than array[small]
					then: set small as j
		5. swap the values of array[small] and array[i]
}

BubbleSort(array[], size)
{
	1. Repeat for i=0 to size-1
		2. Repeat for j=1 to size-1-i
			3. if array[j-1] is greater than array[j]
				then: swap the values of array[j-1] and array[j]
}

InsertionSort(array[], size)
{
	1. Repeat for i=1 to size
		2. set key as array[i]
		3. set j as i-1
		4. Repeat while j>=0 and array[j] > key
			5. set array[j+1] as array[j]
			6. set j as j-1
		7. set array[j+1] as key
}
```

<div style="page-break-after: always; visibility: hidden">
\pagebreak
</div>

## Pseudo-code
```plain
// insertion, bubble and selection sort

# include <stdio.h>
# include <stdlib.h>
# include <time.h>
# include <ctype.h>

void swap(int arr[], int a, int b)
{
	int temp = arr[a];
	arr[a] = arr[b];
	arr[b] = temp;
}

void show_arr(int arr[], int size)
{
	for (int k=0; k<size; k++)
		printf("%3d", arr[k]);
	printf("\n");
}

void bubbleSort(int arr[], int size)
{
	for (int i=0; i<size-1; i++)
	{
		for (int j=1; j<size-1-i; j++)
		{
			if (arr[j-1] > arr[j])
				swap(arr, j-1, j);
		}
		show_arr(arr, size);
	}
}

void selectionSort(int arr[], int size)
{
	int small;
	for (int i=0; i<size-1; i++)
	{
		small = i;
		for (int j=i+1; j<size; j++)
		{
			if (arr[j] < arr[small])
				small = j;
		}
		swap(arr, i, small);
		show_arr(arr, size);
	}
}

void insertionSort(int arr[], int size)
{
	int key, i, j;
	for (i=1; i<size; i++)
	{
		key=arr[i];
		for (j=i-1; j>=0; j--)
		{
			if (arr[j] > key)
				arr[j+1] = arr[j];
			else
				break;
		}
		arr[j+1] = key;
		show_arr(arr, size);
	}
}

int main()
{
	// int arr_S[] = {4,2,7,8,1,5,9,0,3,6};
	// const int size = sizeof(arr_S)/sizeof(int);

	// int arr_B[size];
	// for (int i=0; i<size; i++)
	// 	arr_B[i] = arr_S[i];

	const int size = 10;
	int arr[size], choice;
	char y_n; 
	
	do
	{
		srand(time(0)+rand());
		for (int i=0; i<size; i++)
		{
			arr[i] = rand()%100;
		}
		printf("\nChoose from the following :-\n");
		printf("    1. Selection Sort 
		      \n    2. Bubble Sort 
		      \n    3. Insertion Sort");
		printf("\n\n    Enter choice : ");
		scanf("%d", &choice);

		switch (choice)
		{
			case 1:
			{
				printf("\nSELECTION SORT\n");
				selectionSort(arr, size);
			}
			break;

			case 2:
			{
				printf("\nBUBBLE SORT\n");
				bubbleSort(arr, size);
			}
			break;

			case 3:
			{
				printf("\nINSERTION SORT\n");
				insertionSort(arr, size);
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
    1. Selection Sort
    2. Bubble Sort
    3. Insertion Sort

    Enter choice : 1

SELECTION SORT
 30 36 33 35 89 36 80 88 59 92
 30 33 36 35 89 36 80 88 59 92
 30 33 35 36 89 36 80 88 59 92
 30 33 35 36 89 36 80 88 59 92
 30 33 35 36 36 89 80 88 59 92
 30 33 35 36 36 59 80 88 89 92
 30 33 35 36 36 59 80 88 89 92
 30 33 35 36 36 59 80 88 89 92
 30 33 35 36 36 59 80 88 89 92


Do you wish to continue? (y/n) : y

Choose from the following :-
    1. Selection Sort
    2. Bubble Sort
    3. Insertion Sort

    Enter choice : 2

BUBBLE SORT
 41 54 60 25 61  9 63 20 71  1
 41 54 25 60  9 61 20 63 71  1
 41 25 54  9 60 20 61 63 71  1
 25 41  9 54 20 60 61 63 71  1
 25  9 41 20 54 60 61 63 71  1
  9 25 20 41 54 60 61 63 71  1
  9 20 25 41 54 60 61 63 71  1
  9 20 25 41 54 60 61 63 71  1
  9 20 25 41 54 60 61 63 71  1


Do you wish to continue? (y/n) : y

Choose from the following :-
    1. Selection Sort
    2. Bubble Sort
    3. Insertion Sort

    Enter choice : 3

INSERTION SORT
 26 96 91 94 40 32 62 76 97 50
 26 91 96 94 40 32 62 76 97 50
 26 91 94 96 40 32 62 76 97 50
 26 40 91 94 96 32 62 76 97 50
 26 32 40 91 94 96 62 76 97 50
 26 32 40 62 91 94 96 76 97 50
 26 32 40 62 76 91 94 96 97 50
 26 32 40 62 76 91 94 96 97 50
 26 32 40 50 62 76 91 94 96 97


Do you wish to continue? (y/n) : n

exited program
```

## Analysis
### Selection Sort
The algorithm iterates through the array to find the minimum or maximum elements and it swaps it to its proper location.

Consider an array of length $n$. The minimum/maximum element can be at any index in the array.

To place every element at its proper place, a nested loop is set ip to find the lowest element in the complete array. After the lowest element is found, a subarray is considered which contains all elements besides the one found previously, from which the lowest element is found.

Therefore, we can see that the number of searches are as follows:
$$searches = (n) + (n-1) + ... + 1$$
$$\implies searches = \sum_{i=1}^{n}i = \frac{n(n+1)}{2} = O(n^2)$$
$\therefore$ the obtained time complexity is $O(n^2)$

### Bubble Sort
This algorithm iterates through the array to find out-of-order pair of elements and swap them to the right side repeatedly until the array is sorted.

Consider an array of length $n$. The minimum/maximum element can be at any index in the array.

The array is iterated and all pairs out of order are found and swapped. This leads to the maximum/minimum element being moved to the end of the array. Following this, a subarray excluding the last element is iterated upon and the process repeats until the array is in order.

Therefore, we can see that the number of searches are as follows:
$$searches = (n) + (n-1) + ... + 1$$
$$\implies searches = \sum_{i=1}^{n}i = \frac{n(n+1)}{2} = O(n^2)$$
$\therefore$ the obtained time complexity is $O(n^2)$

<div style="page-break-after: always; visibility: hidden">
\pagebreak
</div>


### Insertion Sort
The algorithm iterates through the array considering it element by element and swap the element to its correct location until the array is fully sorted.

Consider an array of length $n$. The array is divided into two subarrays, one sorted and one unsorted. One by one, elements from unsorted are considered and then they are inserted into the sorted subarray at their correct spot. Hence, we can understand that the sorted subarray grows from 1 element to 2 element and so on until it is $n$ elements long. Therefore, the number of searches needed to insert the element at the correct spot i worst case scenario (i.e. the end of the array) will be:

$$searches = (n) + (n-1) + ... + 1$$
$$\implies searches = \sum_{i=1}^{n}i = \frac{n(n+1)}{2} = O(n^2)$$
$\therefore$ the obtained time complexity is $O(n^2)$
