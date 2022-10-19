# Lab
1. binary and linear recursive search
2. bubble selection and insertion sorts
3. quick and merge sorts
4. MST - prim's and kruskal's
5. greedy - knapsack (frac) and task/activity scheduling
6. dynamic - knapsack (0/1)
7. BFS/DFS

- rest
	- dijkstra
	- N-queen
	- knpasack (backtracking)
	- TSP (branch and bound)
---
# All Algorithms
- [x] ***Basics***
	- [x] linear search
	- [x] bubble sort
	- [x] selection sort
	- [x] insertion sort
- [x] ***Divide and Conquer***
	- [x] binary search
	- [x] merge sort
	- [x] quick sort
	- [x] Strassen method 
- [ ] ***Greedy***
	- [x] MST
		- [x] Prim's
		- [x] Kruskal's
	- [x] Fractional Knapsack
	- [ ] Single source shortest path
		- [ ] Dijkstra's
	- [ ] Travelling salesman
- [ ] ***Dynamic Programming***
	- [x] Longest Common Subsequence
	- [x] 0/1 Knapsack
	- [x] Matrix Chain Multiplication
	- [ ] All pair shortest path
		- [ ] Floyd-Warshall	
	- [ ] Travelling Salesman
	- [ ] Single source shortest path
		- [ ] Bellman-Ford
- [ ] ***Graphs***
	- [ ] Traversals
		- [ ] BFS
		- [ ] DFS
	- [ ] Backtracking
		- [ ] 8-queen
		- [ ] knapsack
	- [ ] branch and bound
		- [ ] 0/1 knapsack
		- [ ] Travelling salesman

---
# EN doubt
1. do we send the frame with empty field?
	- yes
2. what is contained in the ARP request response?
	- the frame of request with the empty field of "Destination MAC Address" now filled with the appropriate value and the frame is sent with "Sender MAC Address" in its place (coz end-device roles are inverted)
	- request is broadcast, reply is unicast
	- request sent before sending the required frame
		- it is a sub-task

# BS
| question | answer |
| -------- | ------ |
| 1        | 2      |
| 2        | 2      |
| 3        | 1      |
| 4        | 3      |
| 5        | 3      |
| 6        | 3      |
| 7        | 3      |
| 8        | 2      |
| 9        | 3      |
| 10       | 3       |
| 11       |  2      |
| 12       |   2     |
| 13       |    2    |
| 14       |     0   |
| 15       |        |
| 16       |       2 |

# embedded git repos
- [ ] git_test
- [x] java
- [ ] python
	- [x] applied_math (published)
	- [x] crop-final (published)
	- [x] datsc (theory)
	- [x] mathplot (theory)
	- [x] wave-final (published)
- [ ] shell
	 - [x] cpu_scheduling (published)

# en expt 9
1. connect PCs to Switch
2. connect Switch to Router (gigabitethernet)
3. connect servers to switch (Fastethernet)
4. router - config - interface - g0/0/0 - port status ON mf
5. `Router(config-if)#ip address 192.168.100.1 255.255.255.0`
6. server0 - services - dhcp - service on - change pool name - add default gateway (prev ip address) - put any IP address in start IP address and put Subnet mask
7. server1 - services - dns - ON
8. server1 - config - dhcp ON
9. server2 - config - dhcp ON
10. server2 - HTTP - edit an HTML page as per requirement and save
11. server1 - DNS - add any name - put the IP address of server2 - add the Domain name
12. open any PC - desktop - web browser - put URL `https://<ip address of server2>` - GO
13. the HTML page set in server2 is shown

>[!NOTE]
>- server0 = dhcp server
>- server1 = dns server
>- server2 = web server

>[!NOTE]
>- 169.254.186.141 server2 ip address



