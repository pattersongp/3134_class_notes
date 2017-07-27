# Data Structures - Session 8, July 26
* homework 3 programming portion due on Monday (session 9) at midnight
* homework 5 will definitely use Codio, homework 4 maybe
* lowest homework grade will be dropped and homework 5 will be shorter than the nominal assignment

<br>__Priority Queues__
* priority queues can have elements added, removed, etc, but is not a FIFO data structure
* each inserted element has an attached priority value to it, with the first dequeued elements being the most important
* having multiple elements with similar priorities will usually result in two kinds of priority queue
* real world applications include hospital lines, airport queues, computer processes
* in unix and unix-based systems, programs have a nice number attached to their processes. The higher nice numbers have lower priorities, lower nice numbers have higher priorities. This is the same model we'll be using for our priority queues.
* priority queues will have two staple methods:
  * insert
  * deleteMin - removes the minimum value
  * utilizing a balanced tree will allow the bost of both inserts and deleteMins to cost O(log(n)). This implementation of a priority queue is known as a binary heap.

<br>__Binary Heaps__
* binary min heaps have two conditions:
  * they must be a complete tree (filled in completely, except the last row which is filled in left to right)
  * the min heap order condition: a node must be less than or equal to its children. By definition, the root of the binary heap will be the smallest value present within the set. There is no specified relationship between the children, only between the parent and child nodes.
    * for a max heap, every node is greater than or equal to its children--we will only be referring to min heaps

<br>__Binary Heaps, Array-Based Representation__
* binary heap representation will be using an array, which means we'll have a fixed length
* location 0 is dead space, the root of the tree will be in location 1
* the left child of index[i] is at $2i$, the right child of index[i] is at $(2*i + 1)$. This system works because of the complete condition of the tree sequentially filling up each of the array indices.
* the parent of index[i] is at $i/2$
* _insert method_ - inserting a smaller element at the bottom of the heap requires a method called percolateUp, which compares the values of the parent versus the prospective insert value. If the parent is smaller than the prospect, then the parent is shifted down and the vacant spot is percolated up. Initially, the inserted value is inserted in the next valid spot at the bottom and is percolated up as necessary to create a valid position for the newly inserted value. In the array representation, the inserted value is compared to its parent index and swapped until it reaches the same valid position. The cost of percolateUp is O-(log(n)) [this will be on the written portion of homework 4]
* _deleteMin method_ - implementing a findMin method would involve a cost of O(1), since it would simply be a removal of the root. Removing the node would only have one possible substitute for the root, which is the last possible node in the last row (to maintain a complete condition). Since our deleteMin method removes the root, we need a percolateDown method to correct the min heap order condition. The smaller of the root's two children is swapped with the substituted root node; this process is repeated until the substituted node is in a valid position to fulfill the complete condition and min heap order condition of the heap. The big-O cost will also be O(log-n) for this method.
* max heap methods will be the exact same, with the exception of the heap order condition (being greater than versus less than)
* _buildHeap_ -  inserting elements from an out-of-order array of values can be done in O(nlog(n)) time--insert values over n and percolateUp over log(n) creates O(nlog(n))--but can be further optimized to be done in linear time. Assume we have an array in an arbitrary order that starts at index 1. We take the midpoint index of the array and percolateDown, from there moving backward through the array and percolating down. Until we make it back to the root, where we know that all of the children nodes and trees are properly heapified.
  * the max amount of percolations that a node might have to do is equal to its height, which means that the total number of percolations in an arbitrarily ordered tree is equal to the sum of the heights of the nodes. Through an extensive proof, it shows that the cost of buildHeap is O(n).
  * _heapSort_ is used to sort an arbritrarily ordered array, with a cost of $O(nlog(n))$. Though usually a max heap is used for heapSort.

<br>__Sorting__
* comparison based sorting algorithms have $O(n^2)$ costs; examples include selection sort and insertion sort
  * _selection sort_ - worst case scenario cycles through $(n + n - 1 + n - 2 + ...) = n(n+1)/2$. Best case scenario still requires cycling through all of the values in the worst case scenario, providing the same order cost. Therefore, in all cases of selection sort, the cost is $O(n^2)$
  * _insertion sort_ - best case scenario is $O(n)$ with a sorted array. Worst case scenario is a backwardly arranged array of values, where each value will have to cycle to the beginning of the sorted portion to be added to it. This provides a $O(n^2)% cost.
* divide and conquer algorithms split the array into two parts and recurse into those two parts; examples include merge sort
  * _merge sort_ - base case involves an empty or array of size 1 (since both of these are sorted and can be checked with a cost of O(1)).
    ``` java
    int[] mergeSort(int[] a) {
      if (a.length<=1)
        return a;

      int[] a1 = mergeSort(1st half of a); // splits a in half
      int[] a2 = mergeSort(2nd half of a); // creating two new arrays

      // this can be done by adding another array, merging within the
      // temp array as storage and placing the values back into the
      // original array to create the sorted array

      return merge(a1, a2);

      // fusing these two arrays would involve creating two variables
      // pointing at the beginning of these arrays and comparing the
      // values, inserting them into an original bigger array

    }
    ```
