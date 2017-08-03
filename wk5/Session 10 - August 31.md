# Data Structures - Session 10, August 2
* raw grades for homework 2 have been made, not posted
* homework 4 solutions will be posted after the grace period passes
* first half of the final coincides with the midterm review sheets
* final questions (so far): recursive method on a tree, coding problem related to binary heaps, AVL balancing problem, inductive proof based on graph properties, possible questions about graph algorithms, smiley face
* homework 5 will be Djikstra's algorithm (use linear pass through, not priority queue)

<br> __Graphs, Continued__
* _sparse_ vs _dense_ graphs - dense is a order of magnitude, meaning that most of the nodes are connected to most other nodes. A complete graph means that every single node is connected to every other node. Sparse graphs mean otherwise (ex: each vertex connected to a single other vertex)
* a _disconnected_ graph is a graph that has any components (nodes or subgraphs) that are not connected via an edge to each other. A _connected_ graph (when speaking about undirected graphs) are graphs that, from any vertex, can find a path to any other vertex.
* a _weakly_ connected graph is a directed, connected graph that is considered connected if the path directions are ignored
* a _strongly_ connected graph is a graph that allows traversal from any node to any other while honoring path directions

<br> __Graph Representation__
* _adjacency matrix_ - a matrix that portrays the adjacency of nodes within a graph
  * using the columns as source vertices and the rows as destination vertices allows us to portray directions
  * the cost of representing a graph with an adjacency matrix is $O(|V|^2)$
* _adjacency list_ - each vertex is represented by an object, or a class vertex. The vertex will have, in one of its fields, a LinkedList. Each element in the LinkedList will have an entry for a vertex it is connected to.
  * the cost of an adjacency list would be $O(|E|)$ for a sparse graph. A a dense graph would cost $O(|V^2|)$.

<br> __Topological Sorting__
* sometimes referred to as topSort, takes a directed acyclic graph (DAG) and provides an ordering of the vertices such that all vertices that a specific vertex is dependent on prior to visiting the actual vertex itself
* in-degree property is going to be the count of how many edges terminate on a specific vertex (ex: with class prerequisites as in-degrees, the in-degree of 1004 would be 0, 3134 would be 1, etc). If starting a DAG without a vertex of in-degree of 0, it must have a cycle. This is an assumed-to-be precalculated value.
  * using the class topSort as an example, picking an initial class with an in-degree of 0 would allow a student to start with a class with no prerequisites. Once picked, decrement its adjacency list by one to create new adjacent class with in-degrees of 0. This allows a progression through the DAG and accounts for all prerequisite classes through a particular path.

<br> __Topological Sort Pseudocode Example__
  ``` java
  void topsort() throws CycleFoundException {
    for(int counter = 0; counter < NUM_VERTICES; counter++) { // this costs O(|V|)
      Vertex v = findNewVertexOfIndegreeZero( ); // this costs O(|V|), bringing the total cost to O(|V|^2)
      if(v == null)
        throw new CycleFoundException();
        v.topNum = counter;
      for each Vertex w adjacent to v
        w.indegree--; // this technically add O(|E|) to the cost, but may or may not get drowned out
  }
  ```

<br> __Shortest Path Algorithms__ - _see Weiss, chapter 9_
* greedy algorithm is an algorithm that, at any given moment, does what appears to be best. For some problems, these algorithms are optimal. Djikstra's algorithm is one of these. The travelling salesman problem may not be optimal. Creating change is also another scenario that utilizes a greedy algorithm.
* Varona's diagram is composed of bisectors between obstacles (or vertices) and creates additional vertices of the intersections of the bisecting lines. Running Djikstra's algorithm along these vertices creates a path finding algorithm that accounts for obstacles.
