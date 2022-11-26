%%[[_Lab Files]]%%
%%#lab\ada%% 
# Open Ended Experiment 1

## Objective
Implementing Matrix Chain Multiplication using Dynamic Programming

## Resources
Python, Numpy

## Theory


## Source Code
```plain
# MATRIX CHAIN MULTIPLICATION
# (Using Dynamic Programming)

# for np.Inf
import numpy as np
# to clear the screen
from os import system

# return matrices of appropriate size
def get_mat(n):
	m = []
	for i in range(n):
		row = [i for i in range(n)]
		m.append(row)
	for i in range(n):
		m[i][0] = m[0][i] = i
	
	return m

# display matrix 'm'
def show(mat):
	print()
	for i in range(len(mat)):
		if i == 0:
			print('m[]|', end=' ')
		else:
			print(f"{mat[i][0]:2} |", end=' ')
		for j in range(i-1):
			print('       ', end=' ')
		
		if i == 0:
			for j in range(1,len(mat)):
				print(f"{mat[i][j]:7}", end=' ')
			print('\n---+', end='')
			for j in range(len(mat)):
				print('-------', end='')
		else:
			for j in range(i,len(mat)):
				print(f"{mat[i][j]:7}", end=' ')
		print()

# display matrix 's'
def show_s(mat):
	print()
	for i in range(len(mat)-1):
		if i == 0:
			print('s[]|', end=' ')
		else:
			print(f"{mat[i][0]:2} |", end=' ')
		for j in range(i-1):
			print('  ', end=' ')
		
		if i == 0:
			for j in range(2,len(mat)):
				print(f"{mat[i][j]:2}", end=' ')
			print('\n---+', end='')
			for j in range(len(mat)-2):
				print('---', end='')
		else:
			for j in range(i+1,len(mat)):
				print(f"{mat[i][j]:2}", end=' ')
		print()	

# display the optimal solution
def print_optimal(s,i,j):
	if i == j:
		print(f'A{i}', end='')
	else:
		print(' ( ', end='')
		print_optimal(s, i,			s[i][j])
		print_optimal(s, s[i][j]+1, j)
		print(' ) ', end='')

# function to draw the table to display information
def table(p):
	print('+-----------+', end='')
	for i in range(len(p)-1):
		print('---------+', end='')

	print('\n|    matrix |', end='')
	for i in range(len(p)-1):
		print(f'    A{i+1}   ', end='|')

	print('\n+-----------+', end='')

	for i in range(len(p)-1):
		print('---------', end='+')

	print('\n| dimension |', end='')
	for i in range(len(p)-1):
		print(f'  {p[i]:2}x{p[i+1]:2} ', end=' |')

	print('\n+-----------+', end='')
	for i in range(len(p)-1):
		print('---------+', end='')

# ------------------------------------

system('cls')
print('\nMATRIX CHAIN MULTIPLICATION \nUSING DYNAMIC PROGRAMMING\n')

# p = [30,35,15,5,10,20,25]
p = [5,10,3,12,5,50,6]

table(p)

n = len(p)
m = get_mat(n)
s = get_mat(n)


for i in range(1,n):
	m[i][i] = 0


for l in range(2,n):
	for i in range(1,n-l+1):
		j = i+l-1
		m[i][j] = np.Inf
		for k in range(i,j-1+1):
			q = m[i][k] + m[k+1][j] + p[i-1]*p[k]*p[j]
			if q < m[i][j]:
				m[i][j] = q
				s[i][j] = k


print('\n')
show(m)
show_s(s)


print('\n\nsolution :-')
print_optimal(s,1,6)
print('\n')
```

## Output
```plain
MATRIX CHAIN MULTIPLICATION 
USING DYNAMIC PROGRAMMING

+-----------+---------+---------+---------+---------+---------+---------+
|    matrix |    A1   |    A2   |    A3   |    A4   |    A5   |    A6   |
+-----------+---------+---------+---------+---------+---------+---------+
| dimension |   5x10  |  10x 3  |   3x12  |  12x 5  |   5x50  |  50x 6  |
+-----------+---------+---------+---------+---------+---------+---------+


m[]|       1       2       3       4       5       6 
---+-------------------------------------------------
 1 |       0     150     330     405    1655    2010 
 2 |               0     360     330    2430    1950 
 3 |                       0     180     930    1770 
 4 |                               0    3000    1860 
 5 |                                       0    1500 
 6 |                                               0 

s[]|  2  3  4  5  6 
---+---------------
 1 |  1  2  2  4  2 
 2 |     2  2  2  2 
 3 |        3  4  4 
 4 |           4  4 
 5 |              5 


solution :-
 (  ( A1A2 )  (  ( A3A4 )  ( A5A6 )  )  ) 
```