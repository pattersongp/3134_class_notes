#Data Structures and Algorithms
**August 2 2017**

##Final
* Read the sections mentioned at the end of the lectures snippets
* coding problem on binary heaps
* AVL problem from the midterm
* graph proof by induction
* problem on the final descirbing a graph with properties like dense, sparse, complete, connected, disconnected, acyclic, cyclic, directed, undirected

##Graphs Continued
* Complete graph is _every_ node is connected to _every_ node
* Dense graph is number of edges on the order of |V|^2
* Sparse graph is number of edges on the order of |V|
* A connected graph is one that has a path to each node
* Weakly connected graphs are directed graphs that we ignore the direction and find a connected graph
* Strongly connected graphs are directed graphs that you can get to every node from any other node

##Representing Graphs

###Adjacency Matrix
* 2-D array
* To represent a graph with an adjacency matrix is big-oh of |V|^2

###Adjacency List
* Each vertex is represented by an object
* entries in the adjacencies: magnitude |E|

####Example:
Vertice | Adjacencies
--------|------------
V_1     | v_2, v_3
v_2     | v_3
v_3     | v_2

###Topological Sorting (TopSort)
* Applies only to Directed Acyclic Graphs DAG's
* A representation of a graph whose vertices have dependencies
* in-degree: A count of how many edges terminate on that vertex
* As we traverse the graph from in-degrees of zero to adjacent vertices, then we use the in-degree of the adjacent vertices by 1
* You can use this algorithm to detect cycles in a graph. If you're ever in a situation while traversing the graph and there are no in-degrees of 0, there is a cycle in the graph
* Magnitude |E| is at best mag |V| and at worst mag |V|^2

###Shortest-Path Algorithms

####Weighted Shortest-Path Algorithm

####Unweighted Shortest-Path Algorithm
* The number of edges needed to traverse is the cost


