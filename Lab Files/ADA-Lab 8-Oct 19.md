%%[[_Lab Files]]%%
%%#lab_ada%% 
%%#incomplete%% 
# Experiment 8
Oct 19, 2022

## Objective
Implement Travelling Salesman Problem using *Branch and Bound* Method

## Resources
C

## Program Logic / Algorithm
```plain
TSP-Branch-n-Bound(G)
{
	1. A = reduced the adjacency matrix
	2. root cost = sum of row and column reductions
	3. for each i in |G.V|
		4. for each j in G.adj[i]
			5. row i and column j of B = inf
			6. B[j,1] = inf
			7. reduce matrix B
			8. cost = root cost + A[i][j] + reduction cost
		9. choose node with least cost
}
```

## Source Code
```plain
// tsp_bc

# include <stdio.h>
# include <stdlib.h>
# include <math.h>
# include <string.h>
# define  z  		INFINITY
# define  size 		10
# define  n_nodes	5

int n = n_nodes+1;
int n_size = n_nodes;
float temp[size][size];
	
void show(float arr[size][size], char name[])
{
	char space[10] = "";
	for (int i=0; i<strlen(name); i++)
        strcat(space, " ");

	printf("\n\n%s : ", name);
	for (int i=0; i<n; i++)
	{
		if (i == 0)
		{
			for (int j=0; j<n; j++)
				if (j == 0)
					printf("%2.0f | ", arr[i][j]);
				else
					printf("%3.0f ", arr[i][j]);
			printf("\n%s   ", space);
			for (int j=0; j<n; j++)
				printf("----");
			printf("--");
		}
		else
		{
			printf("%s   ", space);
			for (int j=0; j<n; j++)
				if (j == 0)
					printf("%2.0f | ", arr[i][j]);
				else
				{
					if (arr[i][j] == INFINITY)
						printf("  %lc ", (wint_t)236);
					else
						printf("%3.0f ", arr[i][j]);
				}

		}	
		printf("\n");
	}
	printf("\n");
}

int reduce(float arr[size][size])
{
	float min, red=0;
	for (int i=1; i<n; i++)
	{
		min = arr[i][1];
		for (int j=1; j<n; j++)
			if (arr[i][j] < min)
				min = arr[i][j];
		
		if (min == INFINITY)
			min = 0;
		red += min;
		
		for (int j=1; j<n; j++)
			arr[i][j] -= min;
	}
	
	for (int j=1; j<n; j++)
	{
		min = arr[1][j];
		for (int i=1; i<n; i++)
			if (arr[i][j] < min)
				min = arr[i][j];
		if (min == INFINITY)
			min = 0;
		for (int i=1; i<n; i++)
			arr[i][j] -= min;
		red += min;
	}
	
	return red;
}

struct neighbour
{
	int node, cost;
} ;

int delete(struct neighbour neighbours[], int val)
{
	int i;
	for (i=0; i<n_size; i++)
		if (neighbours[i].node == val)
			break;
	for (; i<n_size; i++)
		neighbours[i] = neighbours[i+1];
	n_size--;
	return val;
}

void algo(struct neighbour *branch, float mat[size][size], int node, int root_cost)
{
	char c[10];
	int red_cost, total_cost;

	memcpy(temp, mat, size*size*sizeof(float));
	sprintf(c, "(%d,%d)",node,branch->node);

	for (int i=1; i<n; i++)
		temp[node][i] = temp[i][branch->node] = INFINITY;
	temp[branch->node][1] = INFINITY;

	red_cost = reduce(temp);
	total_cost = root_cost + mat[node][branch->node] + red_cost;

	branch->cost = total_cost;
}

int main()
{
	printf("TRAVELLING SALESPERSON PROBLEM \nUsing Branch-&-Bound");
	int root_cost, root_node, node;
	float W[10][10] = {
		{0,  1,  2,  3,  4,  5},
		{1,  z, 20, 30, 10, 11},
		{2, 15,  z, 16,  4,  2},
		{3,  3,  5,  z,  2,  4},
		{4, 19,  6, 18,  z,  3},
		{5, 16,  4,  7, 16, z}
	};

	int *path = (int *) calloc(n_nodes, sizeof(int));
	struct neighbour *neighbours = (struct neighbour*) calloc(n_nodes, sizeof(struct neighbour));
	for (int i=0; i<n_size; i++)
	{
		neighbours[i].node = i+1;
		neighbours[i].cost = -1;
	}

	root_cost = reduce(W);
	show(W, "W");
	printf("root cost = %d", root_cost);

	node = delete(neighbours, 1);
	root_node = node;
	path[0] = root_node;

	printf("\nneighbours : ");
	for (int i=0; i<n_size; i++)
		printf("%d  ", neighbours[i].node);

	printf("\n\n-------------------------------------------\n\n");

	float current_mat[10][10];
	memcpy(current_mat, W, size*size*sizeof(float));
	int k=1;
	// graph traversal begins here
	while (n_size > 0)
	{
		printf("for node %d", node);
		for (int i=0; i<n_size; i++)
		{
			algo(&neighbours[i], current_mat, node, root_cost);
		}
		
		printf("\nneighbours (%d): \n", n_size);
		for (int i=0; i<n_size; i++)
			printf("  %d has cost = %d\n", neighbours[i].node, neighbours[i].cost);
		int min_cost_pos = 0;
		int min_cost_val = neighbours[min_cost_pos].cost;
		for (int i=0; i<n_size; i++)
			if (neighbours[i].cost < min_cost_val)
			{
				min_cost_pos = i;
				min_cost_val = neighbours[min_cost_pos].cost;
			}
		printf("minimum cost = %d at node %d", min_cost_val, neighbours[min_cost_pos].node);
		// once min cost branch is found
			// obtain the (node,branch) matrix from scratch
			// set current_mat to the (node,branch) matrix
		memcpy(temp, current_mat, size*size*sizeof(float));
		for (int i=1; i<n; i++)
			temp[node][i] = temp[i][neighbours[min_cost_pos].node] = INFINITY;
		temp[neighbours[min_cost_pos].node][1] = INFINITY;
		reduce(temp);
		memcpy(current_mat, temp, size*size*sizeof(float));
			// remove that node from neighours[]
			// change node var to current branch
		node = delete(neighbours, neighbours[min_cost_pos].node);
			// change root_cost var to new min_cost_val
		root_cost = min_cost_val;
			// add the chosen node to the path[]
		path[k++] = node;
		printf("\n\n");
	}
	printf("-------------------------------------------\n\n\n");

	printf("Final Path is :\n");
	for (int i=0; i<n_nodes; i++)
		printf("%d -> ", path[i]);
	printf("%d\n", root_node);

	return 0;
}


```

## Output
```plain
TRAVELLING SALESPERSON PROBLEM
Using Branch-&-Bound

W :  0 |   1   2   3   4   5
    --------------------------
     1 |   ∞  10  17   0   1
     2 |  12   ∞  11   2   0
     3 |   0   3   ∞   0   2
     4 |  15   3  12   ∞   0
     5 |  11   0   0  12   ∞

root cost = 25
neighbours : 2  3  4  5

-------------------------------------------

for node 1
neighbours (4):
  2 has cost = 35
  3 has cost = 53
  4 has cost = 25
  5 has cost = 31
minimum cost = 25 at node 4

for node 4
neighbours (3):
  2 has cost = 28
  3 has cost = 50
  5 has cost = 36
minimum cost = 28 at node 2

for node 2
neighbours (2):
  3 has cost = 52
  5 has cost = 28
minimum cost = 28 at node 5

for node 5
neighbours (1):
  3 has cost = 28
minimum cost = 28 at node 3

-------------------------------------------


Final Path is :
1 -> 4 -> 2 -> 5 -> 3 -> 1
```

## Analysis
The worst case for the Travelling Salesperson Problem using Branch and Bound is $O(2^n)$ as we have to explore all the branches in the search space tree.
