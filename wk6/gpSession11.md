
# Data Structures and Algorithms
**August 7, 2017**

## Final Exam
* Dijkstra's Algorithm
* Kruskal's Algorithm
* Proof on Graphs
    - think N(N-1) / 2 maximum edges
* Properties of graphs
* recursive methods on binary search trees
* AVL Tree insertion balance 
* Hashing
    - lamda's
    - schemes with hashing on table size 11
* Coding on a binary heap   
    - we'll be writing code for a binary heap and how the array works specificially
* differences between full, complete, perfect binary trees
* percolate up, percolate down (build heap operation in order(N))
* merge sort, then merge operation
    - coding question
* quicksort worst case is n^2 as it degenerates
* partition algorithm in code
* union and find in the context of Kruskal's algorithm
* topological sorting
    - topsort, queue version, non-queue version
* Minimum Spanning Tree
    - Prim's Algorithm
* **P** vs **NP** and basic, defN of NP-Complete

ASK ABOUT REHASHING

## Graphs Continued

### Minimum Spanning Tree (MST)
* applies to undirected, weighted graphs
* A subset of the graph G, with all of the vertices but only some of the edges
* Its a tree, so it has to be acyclic
* The tree should visit all of the vertices, this is what the word spanning means
* The MST must be the smallest total weight associated with the tree
* Must have at least N-1 edges
* You can have more than 1 MST inside any particular graph G

#### Applications
* TSP approximation within 2 lengths of optimization
* anything with a weighted network basically

#### Algorithms for Solving for
* All of these are greedy algorithms

##### Prim's Algorithm
* Similiar to Dijkstra's without the update
* Only cares about cost to incorporate a node into a tree -- 1 at a time
* Steps
    - Fill the table and start anywhere
    - fill something in, figure out what you can get to, like Dijsktra's
    - fill in the table and see what you can get to, update the tables and continue

vertices | known | d_v | p_v
---------|-------|-----|----
v_1 | T | 0 | Start
v_2 | T | 1 | v_1
v_3 | T | 2 | v_1
v_4 | T | 4 | v_3

##### Kruskal's Algorithms
* Adding edges 1 by 1
* built with a priority queue
    - offer all edges
    - poll
        + Does it cause a cycle?
    - repeat until n-1 edges
* **Steps**
    - start with the minimal cost edge
    - pick the smallest edge that doesn't cause a cycle
    - repeat

#### Disjoint Sets
* Each item is considered in their own set, they're all separate
    - this requires some kind of set identifier
* **Union** Operation between 2 sets
    - We can represent this with trees, that have arrows pointing up rather than down
* **Find** Operation : tells you the set ID of a particular set
* You always call **union** on the **find** of 2 operations

## NP-Completeness
* Chapter 9.7

### P Algorithms
* Most of the algorithms that we've talked about are polynomial time
* **P** is in **NP**

### NP Problems
* non-deterministic polynomial time
* problems that can be solved in polynomial time, if you know the solution already
* Solutions can be **verified** in polynomial time, but the problem cannot be **solved** in polynomial time

### NP-Complete Problems
* Often considered the hardest of the **NP** Problems
* subset of **NP** 
* If you solve one, you can transform it to solve _all_ **NP** problems in polynomial time

### Traveling Salesman Problem TSP
* **NP-Complete**; it is trivially proved to be in **NP**
* Fully connected undirected graph
* visits eery vertex exactly once and returns to the start
* the sum of the weight of the edges--total length-- is less than some arbitrary K
* Variant-1 : NP-Complete ; A bounded version of this problem
* Variant-2 : Cannot verify in polynomial time, without just redoing the entire problem; this is the optimization variant of the TSP
* The MST is the lower bound of the TSP path, it can never be smaller than the TSP.
