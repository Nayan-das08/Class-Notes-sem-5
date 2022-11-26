%%[[_Lab Files]]%%
%%#lab\ada%% 
# Open Ended Experiment 2

## Objective

## Resources
Python, Matplotlib, Pandas, Networkx

## Theory

## Source Code
```plain
# GRAPH COLORING PROGRAM
# (Using Backtracking)

# for command line arguments
from 	sys 		import argv
# to clear the screen
from 	os 			import system
# to set the node_color argument of nx.draw()
import 	pandas 		as pd
# to visulaize the graph
import 	networkx 	as nx
import 	matplotlib 	as mpl
import 	matplotlib.pyplot as plt

# global list, will contain all optimal solutions
solution = []

# initializer function for graph coloring algorithm
def color_em(nodes, W, n_colors):
	# the list of colors is created 
	# as per the number of colors
	colors = list(range(n_colors))

	# list to keep track of the colors of all the nodes
	status = [0]
	[status.append(-1) for x in range(len(nodes))]

	# the recursive graph coloring algorithm
	# for a set of colors is invoked here
	algo(W, nodes, colors, status)

# the backtracking recursive algorithm function
def algo(W, nodes, colors, status):
	# create a copy of status list
	# this is done so that the changes made in a branch
	# are not reflected back to parent invokation of the function
	status_copy = [i for i in status]

	# if the bottom of the branch is reached
	# this means that this would be one of the 
	# optimal solutions obtained from backtracking algorithm
	# thus store the status list containing colors of all the nodes
	if len(nodes) == 0:
		solution.append(status_copy)
		return

	# if the solution is not reached yet
	# then recursively call if possible
	else:
		nodes_copy = [i for i in nodes]
		current_node = nodes_copy.pop(0)

		# get the nodes adjacent to the current node
		row = W[current_node][1:]
		adj = [i+1 for i,x in enumerate(row) if x > 0]

		# for each color that can be assigned to the current node
		# check if the adjacent nodes don't have the 
		# same color as the current node
		for c in colors:
			flag = 1
			for v in adj:
				# if one of the adjacent nodes have the same color 
				# as the current node, do not call the function here
				if status_copy[v] == c:
					flag = 0
					break
			# if the colors are distinct, call the function 
			# and explore the branch further
			if flag == 1:
				# change the color of current node to the chosen color
				status_copy[current_node] = c
				algo(W, nodes_copy, colors, status_copy)


# ----------------------------------

system('cls')
print('\nGRAPH COLORING PROBLEM \nUsing Backtracking')

W = []
n = int(input("\nNumber of nodes : "))

# get the Adjacency Matrix from the user
print('\nEnter the matrix : ')
for i in range(n+1):
	row_s = input('    ')
	row = [int(i) for i in row_s.split()]
	W.append(row)
print()

# variables used throughout the program
edges = []
nodes = W[0][1:]

# check for this many number of colors
n_colors = int(argv[1])

# variables used for obtaining chromatic number
flag = 0
chromatic = 0

# list of number of colors for which the graph is tested
# color_set = list(range(n_colors))


# get edges
for i in range(1,len(W)):
	for j in range(i+1, len(W)):
		if (W[i][j] > 0):
			edges.append([i,j])

print(f"edges: {edges}\n")
print(f"nodes: {nodes}\n")

for i in range(1,n_colors+1):
	# global list, set as empty before solving for each set of color
	solution = []

	# call the initializer function
	color_em(nodes, W, i)
	
	# if chromatic number is not found yet
	if flag == 0:
		# check if number of possible solutions > 0
		if len(solution) > 0:
			# we have determined the chromatic number
			flag = 1
			chromatic = i

	# display the number of possible solutions for each color set
	print(f'  With {i} colors : ', end='')
	if len(solution) == 0:
		print(f'None')
	else:
		print(f'{len(solution)} solutions')

# display the chromatic number of the graph
print(f'\nChromatic number of the graph : {chromatic}')


# display the graph
g = nx.Graph()
g.add_nodes_from(nodes)
g.add_edges_from(edges)
plt.figure()
plt.title(f'Resultant Colored Graph')
nx.draw(g, with_labels=True, node_color=pd.Series(solution[0][1:]),
cmap=mpl.colormaps['Set1'], node_size=750)
plt.savefig(f'graph_pic.png')
plt.show()
plt.close()
```

## Output
```plain
GRAPH COLORING PROBLEM
Using Backtracking

Number of nodes : 7

Enter the matrix :
    0  1  2  3  4  5  6  7
    1  0  1  0  1  1  0  0
    2  1  0  1  0  0  1  1
    3  0  1  0  0  0  0  0
    4  1  0  0  0  0  0  0
    5  1  0  0  0  0  0  0
    6  0  1  0  0  0  0  0
    7  0  1  0  0  0  0  0

edges: [[1, 2], [1, 4], [1, 5], [2, 3], [2, 6], [2, 7]]

nodes: [1, 2, 3, 4, 5, 6, 7]

  With 1 colors : None
  With 2 colors : 2 solutions
  With 3 colors : 192 solutions
  With 4 colors : 2916 solutions
  With 5 colors : 20480 solutions
  With 6 colors : 93750 solutions

Chromatic number of the graph : 2
```

