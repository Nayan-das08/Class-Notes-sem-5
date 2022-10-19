%%[[_Lab Files]]%%
%%#lab/ada%%
%%#incomplete%% 
# Experiment 7
Oct 12, 2022

## Objective
Implement Graph Traversal methods - Breadth First Search and Depth First Search.

## Resources
C

## Program Logic / Algorithm
### DFS
```plain
DFS(W)
{
	1. let stack[1:size(W)], dfs[1:size(W)], visited[1:size(W)]
	2. push(starting node)
	3. for i=1 to n
		4. dfs[i] = pop(stack)
		5. push unvisited neighbours of popped node
	6. return dfs[]
}
```

### BFS
```plain
BFS(W)
{
	1. let queue[1:size(W)], bfs[1:size(W)], visited[1:size(W)]
	2. enqueue(starting node)
	3. for i=1 to n
		4. bfs[i] = dequeue(queue)
		5. enqueue unvisited neighbours of popped node
	6. return bfs[]
}
```

## Source Code
```plain
# include <stdio.h>
# include <stdlib.h>
# include <string.h>

int n;

int check(int arr[], int target)
{
    for (int i=0; i<n; i++)
        if (arr[i] == target) // the neighbouring node is already visited
            return 1;
    return 0;
}

// DFS functions
void show_stack(int stack[], int top)
{
    printf("\nstack : ");
    for (int i=0; i<=top; i++)
        printf("%d  ", stack[i]);
}

void push(int stack[], int *top, int val)
{
    (*top)++;
    stack[(*top)] = val;
}

void pop(int stack[], int *top, int **W, int dfs[], int visited[])
{
    static int n_visited = 0;
    int val = stack[(*top)];
    
    // move top variable down
    (*top)--;

    // put stack[(*top)] in visited
    dfs[n_visited++] = val;

    // push neighbouring nodes of val
    for (int i=1; i<=n; i++)
    {
        if (W[val][i] > 0)
        {
            if (visited[i] == 0)
            {
                push(stack, top, i);
                visited[i] = 1;
            }
        }
    }
}

void depth_first_search(int **W)
{
    int *dfs     = (int *) calloc(n,sizeof(int));
    int *stack   = (int *) calloc(n,sizeof(int));
    int *visited = (int *) calloc(n+1, sizeof(int));
    int top      = -1;

    push(stack, &top, W[0][1]);
    visited[1] = 1;

    for (int i=0; i<n; i++)
        pop(stack, &top, W, dfs, visited);

    printf("\nDFS   : ");
    for (int i=0; i<n; i++)
        printf("%d  ", dfs[i]);
        
    free(dfs);
    free(stack);
}

// BFS functions
void show_queue(int queue[], int front, int rear)
{
    printf("\nqueue : ");
    for (int i=front; i<=rear; i++)
        printf("%d  ", queue[i]);
}

void enqueue(int queue[], int *rear, int val)
{
    (*rear)++;
    queue[(*rear)] = val;
}

void dequeue(int queue[], int *front, int *rear, int **W, int bfs[], int visited[])
{
    static int n_visited = 0;
    int val = queue[(*front)];
    
    // move front variable forward
    (*front)++;

    // put queue[(*front)] in visited
    bfs[n_visited++] = val;

    // enqueue neighbouring nodes of val
    for (int i=1; i<=n; i++)
    {
        if (W[val][i] > 0)
            if (visited[i] == 0)
            {
                enqueue(queue, rear, i);
                visited[i] = 1;
            }
    }
}

void breadth_first_search(int **W)
{
    int *bfs     = (int *) calloc(n,sizeof(int));
    int *queue   = (int *) calloc(n,sizeof(int));
    int *visited = (int *) calloc(n+1, sizeof(int));
    int rear     = -1;
    int front    = 0;

    enqueue(queue, &rear, W[0][1]);
    visited[1] = 1;

    for (int i=0; i<n; i++)
        dequeue(queue, &front, &rear, W, bfs, visited);

    printf("\nBFS   : ");
    for (int i=0; i<n; i++)
        printf("%d  ", bfs[i]);
    
    free(bfs);
    free(queue);
}

int main()
{
	system("cls");
	printf("\nGRAPH TRAVERSAL TECHNIQUES");
    printf("\nDepth First Search & Breadth First Search\n");
	
    printf("\nEnter number of nodes : ");
    scanf("%d", &n);
    
    int **W = (int **) malloc((n+1)*sizeof(int *));
    for (int i=0; i<n+1; i++)
    {
        W[i] = (int *) calloc(n+1, sizeof(int));
    }

    printf("\nEnter Adjacency Matrix:\n");
    for (int i=0; i<n+1; i++)
    {
        for (int j=0; j<n+1; j++)
            scanf("%d", &W[i][j]);
    }

    printf("\n\nNodes : ");
    for (int i=1; i<n+1; i++)
        printf("%d  ", W[0][i]);
    printf("\n");

    depth_first_search(W);
    breadth_first_search(W);

    printf("\n");
	return 0;
}
```

## Output
```plain
GRAPH TRAVERSAL TECHNIQUES
Depth First Search & Breadth First Search

Enter number of nodes : 8

Enter Adjacency Matrix:
0  1  2  3  4  5  6  7  8
1  0  1  0  0  1  0  1  0
2  1  0  1  0  1  1  0  0
3  0  1  0  1  0  1  0  0
4  0  0  1  0  0  1  0  0
5  1  1  0  0  0  1  1  0
6  0  1  1  1  1  0  1  1
7  1  0  0  0  1  1  0  1
8  0  0  0  0  0  1  1  0


Nodes : 1  2  3  4  5  6  7  8

DFS   : 1  7  8  6  4  3  5  2
BFS   : 1  2  5  7  3  6  8  4
```

## Analysis
In Depth First Search, we use the data structure *stack* to navigate or traverse through the graph. The starting node is pushed into the stack first so that the algorithm can start from there. Then, we pop an element and declare that node as fully traversed, while pushing its neighbouring nodes which haven't been visited yet, these nodes are suspended and we pop from the stack again to get the next node to be traversed while pushing neighbouring nodes. This goes on till all the nodes of the graph are popped from the stack. The resulting string would give us the DFS traversal. In this method, we traverse till the depth of a branch and then traverse the adjacent branch before moving to the parent node and following the same steps.

In Breadth First Search, we use the data structure *queue* for traversal through the graph. The starting node is enqueued into the stack first so that the algorithm can start from there. Then, we dequeue an element and declare that node as fully traversed, while enqueueing its neighbouring nodes which haven't been visited yet, these nodes are suspended and we dequeue from the queue again to get the next node to be traversed while enqueueing neighbouring nodes. This goes on till all the nodes of the graph are dequeued from the queue. The resulting string would give us the BFS traversal. In this method, we traverse till the the adjacent nodes of a level first before traversing into the next level of the graph.