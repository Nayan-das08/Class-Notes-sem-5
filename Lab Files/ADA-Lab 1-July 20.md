%%[[_Lab Files]]%%
%%#lab/ada%% 
# Experiment 1
July 20, 2022

## Objective
Implement recursive binary and linear search and determine the time taken to search an element. Repeat for different values of 'n' where 'n' is number of elements in the list to be searched. Plot a graph between time taken and 'n'.

## Resources
C and Python

## Program Logic / Algorithm
```plain
RecursiveLinearSearch(array[], target, loc)
{
	1. if array[loc] = target, then: print "target found at loc"
	   and exit
	3. else: call RecursiveLinearSearch() for loc = loc + 1
}

RecursiveBinarySearch(array[], target, low, high)
{
	1. set m = (low + high) / 2
	2. if low > high, then exit
	else: 
		3. if array[m] = target, then print "target found at loc" 
		   and exit
		   else:
				4. if target lies in the upper half, then 
				   call RecursiveBinarySearch() for high = m - 1
				6. else if target lies in lower half, then 
				   call RecursiveBinarySearch() for low = m + 1
}
```

## Pseudo-code
### C code
```plain
// recursive linear and binary sort

# include <stdio.h>
# include <stdlib.h>
# include <time.h>

const int MAXSIZE = 10000;

int RecLinearSearch(int arr[], int target, int loc, int *step)
{
	(*step)++;
	if (arr[loc] == target)
		return loc;
	else
		return RecLinearSearch(arr, target, loc+1, step);
}

int RecBinarySearch(int arr[], int low, int high,
int target, int *step)
{
	(*step)++;
	int m = (high + low)/2;
	if (low > high)
		return -1;
	else
	{
		if (arr[m] == target)
			return m;
		else
		{
			if (target < arr[m])
				// high needs to move up
				return RecBinarySearch(arr, low, m-1, target, step);
			else
				// low need to move down
				return RecBinarySearch(arr, m+1, high, target, step);
		}	
	}
}

int main()
{
	int arr[MAXSIZE], target_L, target_B, p, step, n=1, k=0;
	FILE *file_linear, *file_binary;
	file_linear = fopen("linear_vals_2.dat", "w");
	file_binary = fopen("binary_vals.dat", "w");
	
	for (n=1; n<=MAXSIZE; n++)
	{
		// get array
		for (int i=0; i<n; i++)
			arr[i] = i*2;
		
		// get random target (for binary)
		srand(time(0)+rand());
		target_B = arr[rand()%n];

		// get last value of array (for linear)
		target_L = arr[n-1];

		// linear search
		step = 0;
		p = RecLinearSearch(arr, target_L, 0, &step);
		fprintf(file_linear, "%d %d\n", n, step);

		// binary search
		step = 0;
		p = RecBinarySearch(arr, 0, n-1, target_B, &step);
		fprintf(file_binary, "%d %d\n", n, step);
	}
	fclose(file_linear);
	fclose(file_binary);
	printf("Linear and Binary Searchs are successfully
	 performed on an array with varying size\n");
	printf("Plotting the graph using python code");
	system("python plot_linear_binary.py");
	return 0;
}
```

### Python code
```plain
import matplotlib.pyplot as plt

x = []
y = []
x2 = []
y2 = []

file = open('linear_vals_2.dat')
for i in file:
	a = i.replace("\n", "")
	x.append(int(a.split(' ')[0]))
	y.append(int(a.split(' ')[1]))

file = open('binary_vals.dat')
for i in file:
	a = i.replace("\n", "")
	x2.append(int(a.split(' ')[0]))
	y2.append(int(a.split(' ')[1]))

plt.plot(x,y)
plt.plot(x2,y2)
plt.xlabel('no. of elements')
plt.ylabel('no. of steps taken')
plt.title('Complexity comparison of linear search and binary search')
plt.legend(['linear search', 'binary search'])
plt.show()
```

## Output
```plain
Linear and Binary Searchs are successfully performed 
on an array with varying size
Plotting the graph using python code
```

## Analysis
The recurrence relation for **Recursive Binary Search** would be
	$T(n)=T(\frac{n}{2})+O(1)$
Now, 
	$T(\frac{n}{2})=T(\frac{n}{4})+O(1)$
	$T(\frac{n}{4})=T(\frac{n}{8})+O(1)$
	$T(\frac{n}{8})=T(\frac{n}{16})+O(1)$
and so on.

Substituting the values of $T(\frac{n}{2})$, $T(\frac{n}{4})$ and $T(\frac{n}{8})$ in $T(n)$
	$T(n)=T(\frac{n}{4})+2\cdot O(1)$
	$T(n)=T(\frac{n}{8})+3\cdot O(1)$
	$T(n)=T(\frac{n}{16})+4\cdot O(1)$

The general form for $k$ iterations :- 
	$T(n)=T(\frac{n}{2^k})+k\cdot O(1)$

After sufficient number of iterations, the size of the last division would be 1.
Thus, $\frac{n}{2^k} = 1$ is the limiting condition for the recurrence relation.
On further solving,
	$2^k=n$
	$k=log_2n$

Therefore, 
	$T(n)=T(1)+log_2n\cdot O(1)$
	$T(n)=O(log_2n)$

Another technique would be *Master Method* for dividing functions :-
We have, 
	$T(n)=T(\frac{n}{2})+O(1)$
	$T(n)=T(\frac{n}{2})+1$, for $O(1)=1$

Now, for $aT(n)=T(\frac{n}{b})+f(n)$, where $f(n)=O(n^klog^pn)$
	$a=1$, $b=2$, $k=0$, $p=0$	
	$log_ba=log_21=0=k$ and $p>-1$

Therefore, $T(n)=\Theta(log(n))$


Similarly, for **Recursive Linear Search**, the recurrence relation :-
	$T(n)=T(n-1)+O(1)$
	$T(n)=T(n-1)+1$, for $O(1)=1$
	
Now, using *Master Method* for Decreasing functions :-
	for $T(n)=aT(n-b)+f(n)$
	$a=1$, $b=1$, $f(n)=1$

Therefore $T(n)=O(n)$

## Graph
![graph](Figure_Lab-1.png)