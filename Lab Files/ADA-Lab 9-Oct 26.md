%%[[_Lab Files]]%%
%%#lab_ada%% 
# Experiment 9
Oct 26, 2022

## Objective
Implement Single Source Shortest Path algorithms - Dijkstra and Bellman-Ford algorithms

## Resources
C

## Program Logic / Algorithm
### Dijkstra's Algorithms
```plain
Dijkstra(G,w,s)
{
	1. S = NULL
	2. Q = G.V
	3. while Q != NULL
		4. u = extract_min(Q)
		5. S = union(S,u)
		6. for each vertex v in G.adj[u]
			7. relax_edge(u,v,w)
}
```

### Bellman-Ford Algorithm
```plain
Bellman-Ford(G,w,s)
{
	1. for i = 1 to |G.V|-1
		2. for each edge (u,v) in G.E
			3. relax_edges(u,v,w)
	4. for each edge (u,v) in G.E
		5. if v.d > u.d + w(u,v)
			6. return false
	7. return true
}
```

## Source Code
### Code for Dijkstra's Algorithm
```plain
// dijkstra

# include <stdio.h>
# include <stdlib.h>
# include <math.h>
# include <string.h>
# define size 10

int n, n_edges=0;

void status(int d[], int S[])
{
	printf("status : \n      ");
    for (int i=1; i<n; i++)
    	printf("%2d  ", i);

    printf("\n  d : ");
    for (int i=1; i<n; i++)
    	if (d[i] == INT_MAX)
    		printf(" %lc  ", (wint_t)236);
    	else
    		printf("%2d  ", d[i]);
    
    printf("\n  S : ");
    for (int i=1; i<n; i++)
        printf("%2d  ", S[i]);
    printf("\n\n");
}

int extract_min(int d[], int S[])
{
    int pos, min=INT_MAX;
    for (int i=1; i<n; i++)
        if (S[i] == 0) // not visited
            if (d[i] < min)
            {
                pos = i;
                min = d[i];
            }
    return pos;
}

int main()
{
	printf("\nDIJKSTRA ALGORITHM \n(Single Source Shortest Path)\n");
	
    // get the adjacency matrix from user
    printf("\nEnter number of nodes : ");
    scanf("%d", &n);
    n++;
    int **W = (int **) malloc((n)*sizeof(int *));
    for (int i=0; i<n+1; i++)
    {
        W[i] = (int *) calloc(n, sizeof(int));
    }

    printf("\nEnter Adjacency Matrix:\n");
    for (int i=0; i<n; i++)
    {
        printf("    ");
        for (int j=0; j<n; j++)
        {
            scanf("%d", &W[i][j]);
        }
    }

    // declare arrays to be used
    int *d = (int *) calloc(n,sizeof(int));
    int *S = (int *) calloc(n,sizeof(int));
    for (int i=1; i<n; i++)
    {
    	d[i] = INT_MAX;
        S[i] = 0;
    }

    // set d[source] as 0
    int source = 1;
    d[source] = 0;

    int current_node;
    for (int i=1; i<n; i++)
    {
        // get node with minimum key
        current_node = extract_min(d,S);

        // set the obtained node as visited
        S[current_node] = 1;
        
        // adjacent nodes
        for (int j=1; j<n; j++)
        {
            if (W[current_node][j] > 0)
            // adjacent nodes
            {
                // edge relaxation
                if (d[current_node] + W[current_node][j] < d[j])
                    d[j] = d[current_node] + W[current_node][j];
                
            }
        } 
    }

    // display result
    printf("\n\nFinal costs from node %d to all nodes :-\n  node : ", source);
    for (int i=1; i<n; i++)
        printf("%2d  ", i);

    printf("\n  cost : ");
    for (int i=1; i<n; i++)
        if (d[i] == INT_MAX)
            printf(" %lc  ", (wint_t)236);
        else
            printf("%2d  ", d[i]);
    
    free(d);
    free(S);
    free(W);
}
```

### Code for Bellman-Ford's Algorithm
```plain
// bellman_ford

# include <stdio.h>
# include <stdlib.h>
# include <math.h>

int n;

void status(int d[])
{
	printf("d[i] : \n  ");
    for (int i=1; i<n; i++)
    	printf("%2d  ", i);
    printf("\n  ");
    for (int i=1; i<n; i++)
    	if (d[i] == INT_MAX)
    		printf(" %lc  ", (wint_t)236);
    	else
    		printf("%2d  ", d[i]);
    printf("\n\n");
}

struct edge
{
	int a,b,wt;
};

int main()
{
	printf("\nBELLMAN-FORD ALGORITHM \n(Single Source Shortest Path)\n");
	
	// get the adjacency matrix from user
    printf("\nEnter number of nodes : ");
    scanf("%d", &n);
    n++;
    int **W = (int **) malloc((n)*sizeof(int *));
    for (int i=0; i<n+1; i++)
    {
        W[i] = (int *) calloc(n, sizeof(int));
    }

    printf("\nEnter Adjacency Matrix:\n");
    for (int i=0; i<n; i++)
    {
        printf("    ");
        for (int j=0; j<n; j++)
        {
            scanf("%d", &W[i][j]);
        }
    }

    struct edge *edges = (struct edge *) calloc((n*n), (sizeof(struct edge)));

    int k=0, n_edges;
    for (int i=1; i<n; i++)
    {
    	for (int j=1; j<n; j++)
    		if (W[i][j] != 0)
            {
                edges[k].a = i;
                edges[k].b = j;
                edges[k].wt = W[i][j];
                k++;
            }
    }
    n_edges = k;

    int *d = (int *) calloc(n,sizeof(int));
    for (int i=1; i<n; i++)
    	d[i] = INT_MAX;

    // set d[source] as 0
    int source = 1;
    d[source] = 0;

    int u,v,w,flag=1;
    for (int i=1; i<(n-1); i++)
    {
    	for (int j=0; j<n_edges; j++)
    	{
    		// get edge
    		u = edges[j].a;
    		v = edges[j].b;
    		w = edges[j].wt;

    		// edge relaxation
    		if (d[u] + w < d[v])
                    d[v] = d[u] + w;
    	}
    }
    // checking for negative weight cycles
    for (int j=0; j<n_edges; j++)
	{
		u = edges[j].a;
		v = edges[j].b;
		w = edges[j].wt;

		if (d[u] + w < d[v])
            flag = 0;
	}

	// if no negative weight cycles found
	if (flag == 1)
	{
		printf("\n\nFinal costs from node %d to all nodes :-\n  node : ", source);
    for (int i=1; i<n; i++)
        printf("%2d  ", i);

    printf("\n  cost : ");
    for (int i=1; i<n; i++)
        if (d[i] == INT_MAX)
            printf(" %lc  ", (wint_t)236);
        else
            printf("%2d  ", d[i]);
	}
	else
		printf("\n\nNegative weight cycles found
		\nBellman-Ford Algorithm has failed here");

	free(d);
	free(W);
}
```

## Output
### Output for Dijkstra's Algorithms
```plain
DIJKSTRA ALGORITHM
(Single Source Shortest Path)

Enter number of nodes : 6

Enter Adjacency Matrix:
    0 1 2 3 4 5 6
    1 0 2 4 0 0 0
    2 0 0 1 7 0 0
    3 0 0 0 0 3 0
    4 0 0 0 0 0 1
    5 0 0 0 2 0 5
    6 0 0 0 0 0 0


Final costs from node 1 to all nodes :-
  node :  1   2   3   4   5   6
  cost :  0   2   3   8   6   9
```

### Output for Bellman-Ford Algorithm
```plain
BELLMAN-FORD ALGORITHM
(Single Source Shortest Path)

Enter number of nodes : 5

Enter Adjacency Matrix:
    0  1  2  3  4  5
    1  0  6  0  7  0
    2  0  0  5  8 -4
    3  0 -2  0  0  0
    4  0  0 -3  0  9
    5  2  0  7  0  0


Final costs from node 1 to all nodes :-
  node :  1   2   3   4   5
  cost :  0   2   4   7  -2
```

## Analysis
Dijkstra's Algorithm gives the solution for Single Source Shortest Path problem in a greedy approach while Bellman-Ford is a dynamic programming solution. Dijkstra relaxes the edges of those nodes where the cost is the minimum, thus acting in a greedy way to move to the next node, while Bellman-Ford relaxes all the edges simultaneously certain number of times. 

For Dijkstra, time complexity is given by $\Theta((|V|+|E|)log|V|)$ whereas for Bellman-Ford, we have $O(|V| \cdot |E|)$.