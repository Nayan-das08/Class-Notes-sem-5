%%[[_Lab Files]]%%
%%#lab/ada%%  
# Experiment 4
Sep 14, 2022

## Objective
Implement Prim's and Kruskal's Algorithm for finding the Minimum Spanning Tree (MST) of a graph.

## Resources
C

## Program Logic / Algorithm
### Kruskal's Algorithm
```plain
Kruskal(G,w)
{
	1. A <- null
	2. for each vertex v in G[V]
		3. Make_set(v)
	4. sort edges of E into non-decreasing
	   order of weights w
	5. for each edge (u,v) in G[E]
		6. if Find_set(u) != Find_set(v)
			7. A <- A U (u,v)
			8. Union(u,v)
	9. return A
}
```

### Prim's Algorithm
```plain
Prim(G,w,r)
{
	1. A <- null
	2. for each vertex v in G[V]
		3. key[v] <- infinity
		4. parent[v] <- null
	5. key[r] <- 0
	6. Q <- G[V]
	7. while Q != null
		8. u <- min(Q) by key value
		9. Q <- Q-u
		10. if parent[u] != null
			11. A <- A U (u, parent[u])
		12. for each v in Adjacent(u)
			13. if v is in Q and w(u,v) < key[v]
				14. parent[v] = u
				15. key[v] = w
	16. return A
}
```

## Source-code
### Code for Kruskal's Algorithm
```plain
# include <stdio.h>
# include <stdlib.h>
# include <string.h>

int n_set;

struct edges
{
	int a,b,w;
} edge[105], MST_edge[105];


// QUICK SORT
void swap(struct edges arr[], int i, int j)
{
	struct edges temp = arr[i];
	arr[i] = arr[j];
	arr[j] = temp;
}

int partition(struct edges arr[], int p, int r)
{
	int pivot = arr[r].w; // setting last element as pivot
	int i=p;
	for (int j=p; j<r; j++)
		if (arr[j].w <= pivot)
			swap(arr, i++, j);
	swap(arr, i, r); 
	return i;
}

void quick(struct edges arr[], int p, int r)
{
	int q;
	if (p < r)
	{
		q = partition(arr, p, r);
		quick(arr, p, q-1);
		quick(arr, q+1, r);
	}
}


struct list
{
	int size;
	int *arr;
};

void define(struct list *x)
{
	x->size = 0;
	x->arr = (int *) calloc(x->size+1, sizeof(int));
}

void append(struct list *x, int n)
{
	x->arr = realloc(x->arr, (++x->size)*sizeof(int));
	x->arr[x->size-1] = n;
}

void show_set(struct list set[])
{
	for (int i=0; i<n_set; i++)
	{
		printf("[");
		for (int j=0; j<set[i].size; j++)
			printf("%d  ", set[i].arr[j]);
		printf("\b\b]  ");
	}
	printf("\n");
}

int find_set(struct list set[], int u)
{
	for (int i=0; i<n_set; i++)
		for (int j=0; j<set[i].size; j++)
			if (set[i].arr[j] == u)
				return i;
}

void delete(struct list set[], struct list x)
{
	int i;
	for (i=0; i<n_set; i++)
		if (memcmp(set[i].arr, x.arr, x.size) == 0)
			break;

	for (; i<n_set; i++)
		set[i] = set[i+1];
	n_set--;
}
void union_set(struct list set[], int p, int q)
{
	struct list a, b;
	a = set[p];
	b = set[q];
	delete(set, a);
	delete(set, b);
	for (int i=0; i<b.size; i++)
		append(&a, b.arr[i]);
	n_set++;
	set[n_set-1] = a;
}

int main()
{
	int mat[15][15] = {
		{0,1,2,3,4,5,6,7,8},
		{1,0,5,0,0,4,0,6,0},
		{2,5,0,3,0,2,4,0,0},
		{3,0,3,0,2,0,1,0,0},
		{4,0,0,2,0,0,2,0,0},
		{5,4,2,0,0,0,6,3,0},
		{6,0,4,1,2,6,0,7,4},
		{7,6,0,0,0,3,7,0,8},
		{8,0,0,0,0,0,4,8,0},
	};

	int n=8;
	n_set = n;

	// get edges
	int k=0;
	for (int i=1; i<n; i++)
	{
		for (int j=i+1; j<=n; j++)
		{
			if (mat[i][j] > 0)
			{
				edge[k].a = i;
				edge[k].b = j;
				edge[k].w = mat[i][j];
				k++;
			}
		}
	}

	int n_edges = k;
	
	// sort edges
	quick(edge, 0, k-1);

	// display edges
	printf("edges in the graph are :-\n");
	for (int i=0; i<n_edges; i++)
		printf("    %d, %d   -> %d\n", edge[i].a, edge[i].b, edge[i].w);


	// struct list set[n_set];
	struct list *set = (struct list*) malloc(n_set*sizeof(struct list));
	for (int i=0; i<n_set; i++)
		// set[i] = (int *) calloc(n, sizeof(int));
		define(&set[i]);

	for (int i=0; i<n; i++)
		append(&set[i],i+1);

	printf("\n\n");
	show_set(set);

	int u,v,p,q;
	int n_MST = 0;
	int cost=0; 
	printf("\n\n");
	for (int i=0; i<k; i++)
	{
		u = edge[i].a;
		v = edge[i].b;
		p = find_set(set,u);
		q = find_set(set,v);
		printf("%d found in set no. %d\n", u, p);
		printf("%d found in set no. %d\n", v, q);
		// printf("%d,%d  ->  %d,%d\n", u, v, p, q);
		if (p != q)
		{
			union_set(set,p,q);
			show_set(set);
			MST_edge[n_MST++] = edge[i];
			cost+=edge[i].w;
		}
		else
			printf("found in same set, thus rejected\n");	
		printf("\n\n");
	}

	printf("edges in the MST :-\n");
	for (int i=0; i<n_MST; i++)
		printf("    %d, %d   -> %d\n", MST_edge[i].a, MST_edge[i].b, MST_edge[i].w);

	printf("\n\ncost of MST = %d", cost);

	int MST[15][15];

	for (int i=0; i<15; i++)
		for (int j=0; j<15; j++)
			MST[i][j] = 0;

	for (int i=0; i<n+1; i++)
	{
		MST[0][i] = i;
		MST[i][0] = i;
	}

	for (int i=0; i<n_MST; i++)
	{
		u = MST_edge[i].a;
		v = MST_edge[i].b;
		MST[u][v] = MST_edge[i].w;
		MST[v][u] = MST_edge[i].w;
	}

	printf("\n\nAdjacency Matrix of MST :-\n");
	for (int i=0; i<n+1; i++)
	{
		printf("    ");
		if (i == 0)
		{
			printf("0 | ");
			for (int i=1; i<=n; i++)
				printf("%d  ", i);
			printf("\n  ----+-");
			for (int i=1; i<=n; i++)
				printf("---");
			printf("\n");
			continue;
		}
		for (int j=0; j<n+1; j++)
		{
			if (MST[i][j] == 0)
				printf("-  ");
			else
				printf("%d  ",MST[i][j]);
			if (j == 0)
				printf("\b| ");
		}
		printf("\n");
	}
}
```

### Code for Prim's Algorithm
```plain
# include <stdio.h>
# include <stdlib.h>
# include <math.h>
# include <string.h>
# define w(u,v) mat[u][v]


int n;
int n_Q;

struct edges
{
	int a,b,w;
} MST_edge[28];

struct vertex
{
	int parent, name;
	float key;
};

// QUICK SORT
void swap(struct vertex arr[], int i, int j)
{
	struct vertex temp = arr[i];
	arr[i] = arr[j];
	arr[j] = temp;
}

int partition(struct vertex arr[], int p, int r)
{
	float pivot = arr[r].key; // setting last element as pivot
	int i=p;
	for (int j=p; j<r; j++)
		if (arr[j].key <= pivot)
			swap(arr, i++, j);
	swap(arr, i, r); 
	return i;
}

void quick(struct vertex arr[], int p, int r)
{
	int q;
	if (p < r)
	{
		q = partition(arr, p, r);
		quick(arr, p, q-1);
		quick(arr, q+1, r);
	}
}


void delete(struct vertex u, struct vertex Q[])
{
	int val = u.name;
	int i;
	for (i=0; i<n_Q; i++)
		if (Q[i].name == val)
			break;
	for (; i<n_Q; i++)
		Q[i] = Q[i+1];
	n_Q--;
}

void show_V(struct vertex V[])
{
	printf("\n\n");
	for (int i=0; i<n; i++)
		printf("%d  \tkey = %0.0f  \tparent = %d\n", V[i].name, V[i].key, V[i].parent);
}

void show(struct vertex Q[])
{
	printf("\n\n");
	for (int i=0; i<n_Q; i++)
		printf("%d  \tkey = %0.0f  \tparent = %d\n", Q[i].name, Q[i].key, Q[i].parent);
}

void show_vertex(struct vertex u)
{
	printf("%d  \tkey = %0.0f  \tparent = %d\n", u.name, u.key, u.parent);
}

int get_index_Q(int x, struct vertex Q[])
{
	for (int i=0; i<n_Q; i++)
	{
		if (Q[i].name == x)
			return i;
	}
} 

int get_adj(struct vertex u, int mat[][15], struct vertex V[], struct vertex adj[])
{
	int k=0, x=u.name, count=0, index;
	for (int i=1; i<n+1; i++)
	{
		if (mat[x][i] != 0)
		{
			adj[k++] = V[i-1];
			count++;
		}
	}
	return count;
}

struct vertex min(struct vertex Q[])
{
	quick(Q,0,n_Q-1);
	return Q[0];
}

int v_in_Q(struct vertex v, struct vertex Q[])
{
	for (int i=0; i<n_Q; i++)
		if (Q[i].name == v.name)
			return 1;
	return 0;
}

void update_Q(struct vertex Q[], struct vertex v)
{
	for (int i=0; i<n_Q; i++)
		if (Q[i].name == v.name)
		{
			Q[i].key = v.key;
			Q[i].parent = v.parent;
			break;		
		}
}

void update_V(struct vertex V[], struct vertex v)
{
	int i = v.name;
	V[i-1].key = v.key;
	V[i-1].parent = v.parent;
}

int main()
{
	int mat[15][15] = {
		{0,1,2,3,4,5,6},
		{1,0,4,0,0,0,2},
		{2,4,0,6,0,0,3},
		{3,0,6,0,3,0,1},
		{4,0,0,3,0,2,0},
		{5,0,0,0,2,0,4},
		{6,2,3,1,0,4,0}
	};

	n = 6;
	struct vertex *Q = (struct vertex *) malloc(n*sizeof(struct vertex));
	for (int i=0; i<n; i++)
	{
		Q[i].name	= i+1;
		Q[i].key 	= INFINITY;
		Q[i].parent = 0; 
	}
	Q[0].key = 0;

	struct vertex *V = (struct vertex *) malloc(n*sizeof(struct vertex));
	memcpy(V,Q,n*sizeof(struct vertex));

	n_Q = n;

	int n_adj, n_MST=0;
	struct vertex u, v;
	struct vertex *adj = (struct vertex *) malloc(n*sizeof(struct vertex));
	// -----------------algorithm starts here-----------------
	
	while (n_Q > 0)
	{
		u = min(Q);
		// show_vertex(u);

		delete(u,Q);
		// show(Q);

		if (u.parent != 0)
		{
			MST_edge[n_MST].a = u.name;
			MST_edge[n_MST].b = u.parent;
			MST_edge[n_MST].w = w(u.name, u.parent);
			n_MST++;
		}

		n_adj = get_adj(u, mat, V, adj);

		// printf("\n\nadj :-\n");
		for (int i=0; i<n_adj; i++)
		{
			v = adj[i];
			// printf("%d",v.name);
			if ((v_in_Q(v,Q)) && (w(u.name, v.name) < v.key))
			{
				// printf(" in Q", v.name);
				v.parent = u.name;
				v.key = w(u.name, v.name);
				update_Q(Q,v);
				update_V(V,v);
			}
			// printf("\n");
		}
		// show(Q);
		// printf("\n---------------------------------------\n\n");
	}

	printf("Edges in MST :-\n");
	for (int i=0; i<n_MST; i++)
	{
		printf("    %d, %d   -> %d\n", MST_edge[i].a, MST_edge[i].b, MST_edge[i].w);
	}

	// ---------------------Adjacency Matrix for MST---------------------
	int a, b, cost=0;;
	int MST[15][15];

	for (int i=0; i<15; i++)
		for (int j=0; j<15; j++)
			MST[i][j] = 0;

	for (int i=0; i<n+1; i++)
	{
		MST[0][i] = i;
		MST[i][0] = i;
	}

	for (int i=0; i<n_MST; i++)
	{
		a = MST_edge[i].a;
		b = MST_edge[i].b;
		MST[a][b] = MST_edge[i].w;
		MST[b][a] = MST_edge[i].w;
		cost += MST_edge[i].w;
	}

	printf("\n\ncost of MST = %d", cost);
	printf("\n\nAdjacency Matrix of MST :-\n");
	for (int i=0; i<n+1; i++)
	{
		printf("    ");
		if (i == 0)
		{
			printf("0 | ");
			for (int i=1; i<=n; i++)
				printf("%d  ", i);
			printf("\n  ----+-");
			for (int i=1; i<=n; i++)
				printf("---");
			printf("\n");
			continue;
		}
		for (int j=0; j<n+1; j++)
		{
			if (MST[i][j] == 0)
				printf("-  ");
			else
				printf("%d  ",MST[i][j]);
			if (j == 0)
				printf("\b| ");
		}
		printf("\n");
	}

	return 0;
}
```

## Output
### Kruskal's Algorithm Output
```plain
edges in the graph are :-
    3, 6   -> 1
    3, 4   -> 2
    2, 5   -> 2
    4, 6   -> 2
    2, 3   -> 3
    5, 7   -> 3
    1, 5   -> 4
    2, 6   -> 4
    6, 8   -> 4
    1, 2   -> 5
    5, 6   -> 6
    1, 7   -> 6
    6, 7   -> 7
    7, 8   -> 8


[1]  [2]  [3]  [4]  [5]  [6]  [7]  [8]


3 found in set no. 2
6 found in set no. 5
[1]  [2]  [4]  [5]  [7]  [8]  [3  6]


3 found in set no. 6
4 found in set no. 2
[1]  [2]  [5]  [7]  [8]  [3  6  4]


2 found in set no. 1
5 found in set no. 2
[1]  [7]  [8]  [3  6  4]  [2  5]


4 found in set no. 3
6 found in set no. 3
found in same set, thus rejected


2 found in set no. 4
3 found in set no. 3
[1]  [7]  [8]  [2  5  3  6  4]


5 found in set no. 3
7 found in set no. 1
[1]  [8]  [2  5  3  6  4  7]


1 found in set no. 0
5 found in set no. 2
[8]  [1  2  5  3  6  4  7]


2 found in set no. 1
6 found in set no. 1
found in same set, thus rejected


6 found in set no. 1
8 found in set no. 0
[1  2  5  3  6  4  7  8]


1 found in set no. 0
2 found in set no. 0
found in same set, thus rejected


5 found in set no. 0
6 found in set no. 0
found in same set, thus rejected


1 found in set no. 0
7 found in set no. 0
found in same set, thus rejected


6 found in set no. 0
7 found in set no. 0
found in same set, thus rejected


7 found in set no. 0
8 found in set no. 0
found in same set, thus rejected


edges in the MST :-
    3, 6   -> 1
    3, 4   -> 2
    2, 5   -> 2
    2, 3   -> 3
    5, 7   -> 3
    1, 5   -> 4
    6, 8   -> 4


cost of MST = 19

Adjacency Matrix of MST :-
    0 | 1  2  3  4  5  6  7  8
  ----+-------------------------
    1 | -  -  -  -  4  -  -  -
    2 | -  -  3  -  2  -  -  -
    3 | -  3  -  2  -  1  -  -
    4 | -  -  2  -  -  -  -  -
    5 | 4  2  -  -  -  -  3  -
    6 | -  -  1  -  -  -  -  4
    7 | -  -  -  -  3  -  -  -
    8 | -  -  -  -  -  4  -  -
```

### Prim's Algorithm Output
```plain
Edges in MST :-
    5, 1   -> 4
    2, 5   -> 2
    7, 5   -> 3
    3, 2   -> 3
    6, 3   -> 1
    4, 3   -> 2
    8, 6   -> 4


cost of MST = 19

Adjacency Matrix of MST :-
    0 | 1  2  3  4  5  6  7  8
  ----+-------------------------
    1 | -  -  -  -  4  -  -  -
    2 | -  -  3  -  2  -  -  -
    3 | -  3  -  2  -  1  -  -
    4 | -  -  2  -  -  -  -  -
    5 | 4  2  -  -  -  -  3  -
    6 | -  -  1  -  -  -  -  4
    7 | -  -  -  -  3  -  -  -
    8 | -  -  -  -  -  4  -  -
```

## Analysis
In Kruskal's Algorithm for finding the Minimum Spanning Tree (MST), we sort the edges on the basis of their associated weights as per Greedy Approach. Then we traverse through the list of sorted edges and select the edges which do not form any form of cyclic loops in the formed graph. To maintain the non-cyclic nature of the graph formed with this method, we use sets for each vertices in the beginning. As vertices are connected together, we apply union operation of the sets getting joined together. For checking the validity of an edge while traversal we check if the two vertices are present in same set or not. If they are not in the same set we select them for the MST.

Another method to determine the MST is Prim's Algorithm. In this method we set two values - "key" and "parent" as infinity and null respectively for each vertex. Only for the starting vertex the key value is set as 0. Then, we obtain the vertex having lowest key value in the unvisited portion of the graph (say, $u$). For the vertex $u$ we determine the adjacent vertices $v$ and for each of the adjacent vertices, if it is unvisited and the weight associated with the edge from $u$ and $v$ i.e., $w(u,v)$ is less than key value of $v$, we update the values of $v$ in a way so that its parent gets value $u$ and its key gets value $w(u,v)$. Now if the parent value of vertex $u$ is not null, then we select the ordered pair of $(u,parent[u])$ for the MST.

For both the algorithms, the Worst Case Time Complexity is found to be $O(E\cdot log(V))$.