# Data Structures - Session 9, July 31
* homework 4 will come out tonight
* homework 5 can be submitted by the Friday after the final (August 11)
* AVL tree and recursive coding will be on the final
* know chapter 6 through 6.3
* for chapter 7, skip 7.4 and focus on algorithms and the reading on lower bounds for simple sorting algorithms
* skipping chapter 8 (disjoint sets) for now, just read the first three pages of it to gain API familiarity for disjoint sets
* for chapter 9, we're looking at 9.1, 9.2, first half of 9.3, 9.5, and 9.7
* we did not get to cover Huffman coding, which is in a regular DS curriculum

* Wednesday: adjacency, strongly/weakly connected graph, topological sorting,

<br> __Mergesort__
* If $T(N)$ is the cost of running mergesort on an input of size N, then the cost of running mergesort on input size $N/2$ = $T(N)$. The method is called twice and the cost of merging the input is N. Therefore the equation we have is:
  <br>$T(N)$ = $2*T(N/2) + N$
  <br> divide by two for first call: $T(N)/N$ = $T(N/2)/(N/2)$ + 1
  <br> divide by two again (second call): $T(N/2)/(N/2)$ = $T/N/4)/(N/4)$ + 1
  <br> and so on and so forth.
  * the equations collapse and everything simplifies to <br>$T(N)$ = 1 + $log_2N$, or $T(N)$ = $N$ + $Nlog_2N$

<br> __Quicksort__
* divide and conquer algorithm that can be done in place, as opposed to creating a temporary array (as is necessary with some other algorithms)
* this gives it a slight boost in terms of speed as it doesn't have to copy over elements
* the time complexity is actually O($N^2$) for the (very rare) worst case scenario. Most of the time, it is $O(NlogN)$.
* the goal of quicksort is to find a pivot value and to pivot all values around that value. The two subarrays (larger and smaller) can be recursively sorted through after chooseing the pivot value.
* The pivot value is randomly picked with hope that it'll be the median value. The issue is, quicksort will degenerate into selectionsort if the largest or smallest value is picked, losing the cost advantage it has over other algorithms.
  * the way to bypass this is to pick a pivot using the "median of three": look at the first element of the array, the middle, and the end and find the median amongst those.

<br> __Quicksort Example__
  * ```3 5 2 7 4 6 8 1```
  * using the median of three, we're looking at 3, 7, and 1 and using 3 since it's in the middle of the three
  * pushing the pivot to the end gives us: ``` 1 5 2 7 4 6 8 (3) ```
    * we'll set an index variable, i, at the beginning of the array and another, j, at the end. We'll increment these two inward until they point at a value that is at the wrong side of the pivot value. Once they find these values, they'll swap the values and increment again. Once i and j have crossed, we'll have taken care of all the elements. We then swap the pivot with the i marker (since we know that it's pointing at value larger than the pivot). This gives us ```1 2 (3) 7 4 6 8 5```
  * using the median of three on the second sub-array gives us 6. Running the quicksort swap on this sub-array gives us (after a single swap):
  5 4 (6) 8 7
  * once we get a small enough array, we can use insertionsort to sort the input

<br> __Graphs__
* $G = {V, E}$, graphs are defined by its vertices and edges
* undirected edges don't require an order, undirected graphs contain undirected edges
  * order matters in a directed graph
* two vertices are considered adjacent if there is a path from one to another
* edges can have a cost, or a weight, associated with them. A weighted graph will have various weights for different paths.
* a path in a graph is a sequence of vertices that you visit. The length of the path is (the number of vertices - 1).
  * a cycle is a path that returns to its starting vertex
  * a simple path is such that all the vertices are distinct. A simple path can return to its originating vertex.
* a directed graph is a cyclic graph if there are no undirected graphs in it
  * a directed acyclic graph is also known as a DAG
* a disconnected graph may have a vertex that may have a vertex that is not adjacent to any other vertex
* a sparse graph is a graph whose |E| is on the order of |V|
