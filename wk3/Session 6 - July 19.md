# Data Structures - Session 6, July 19
* Homework 1 solutions are posted
* lecture summaries updated with Monday's lecture with link of AVL tree viewer
* Example of AVL tree question: be able to insert a given element into an AVL tree and show location + rotation of tree post-insertion
* chapter 4.6 talks about tree traversals, might be worth it to read, but no specific comments

<br>__Maps__
* maps have two generics, as the key and value can both be generic data types
* tree maps have an underlying tree structure and hash maps have underlying hash table structures
* a hash value is basically a piece of data with an applied mathematical function (hash function) to provide a certain value. The provided value will then be relatively unique to the input data.
* good hashing will provide wildly different hash value for similar objects, even if they are very similar
* MD5 file hashing is an example of hash functions used to verify file integrity
* encryption is another example, using hash functions to encrypt user passwords

<br>__Hashing__
* Example: hash functions
  ``` java
  public static int hash( String key, int tableSize ) {
    int hashVal = 0;
    for( int i = 0; i < key.length( ); i++ )
      hashVal += key.charAt( i );
    return hashVal % tableSize;
  }
  ```
    * a value must be modded by the hash table size to find a suitable place for it in the table
    * stores similar values in close proximity, plus mispelled words (cat, tac) will be placed in the same place in the table
  ``` java
    public static int hash( String key, int tableSize ) {
      return ( key.charAt( 0 ) + 27 * key.charAt( 1 ) +
        729 * key.charAt( 2 ) ) % tableSize;
    }
  ```
    * takes into account first 3 characters and their order, multiplies them against hardcoded values. This is another example of a bad hash function since words with the same first three letters would be placed in the same place in the table (cat, cathode)
    * using prime numbers for hash values minimizes collisions
* separate chaining - provides a LinkedList value for each place in the hash table, so that the initial value would be linked to the next value, preventing collisions with similarly positioned hashed values. This operation uses inserts for LinkedList, maintaining a constant cost. For contains, the cost might be O(n).
* load factor ($\lambda$) - the ratio of the number of elements divided by the number of spaces in the hash tables (3 elements with 10 spaces provides a load factor of 0.3). $\lambda$ could be a value bigger than one based on the LinkedList hash table model.
  * once the $\lambda$ becomes larger than one, you rehash, or create a new table twice the size of the old table. This involves taking the values of the old hash table and rehash them using the new table size to provide new placements.
  * usually creating a new, larger table wouldn't simply involve doubling the size; it would involve doubling the size and scaling up to the next prime number

<br>__End of Midterm Material__
____

<br>__Midterm Logistics__
* test will be at 5:30pm on Monday, session 7, during the first half of class (ends at 7pm)
* closed book, closed notes, no calculators
* 6 or 7 problems with multiple parts (including a tricky hash table function); questions will be exhaustive
  * AVL tree question, induction tree, recursive method on a binary tree, question on Big-O costs on an algorithm, hash table function question
* problems will be a mixture of short answer questions (might have to write code to achieve a cost, or to derive the cost of an algorithm)
* methods to implement methods we've seen, first question will be induction proof on BST properties (leaves or nodes)
* AVL tree insertion problem with a sequence of numbers, with drawings of tree post-insertions
* recursive method that has something to do with a BSTs, method for a LinkedList

<br>__Midterm Material__
* chapter 1: induction proofs, recursion, generics (as we've used them)
  * basic proofs by induction, proofs by counterexample (probably not on midterm)
  * recursion, design rules of recursion, tower of Hanoi example
  * generics (to the extent that we've used them)
  * what a nested class is, difference between a static nested class vs non-static
* chapter 2: pretty much in entirety, through 2.42
  * Big-Oh notation for asymptotic running times
  * definition for Big-O/Big-$\Theta$/Big-$\Omega$
  * remember distinction for worst/best/average case analyses, if statements between two algorithms (pick the largest of the two)
  * Big-Oh on recursive statements
  * Big-Oh speed comparisons (slowest to fastest, will be on the test)
* chapter 3: entirety, lists, LinkedLists, ArrayLists, implementations, stacks, queues, etc
  * list ADT, list operations
  * ArrayLists, costs for inserts/removes
  * singly and doubly LinkedLists, costs for inserts/removes (based on starting points or with direct reference to node)
  * sentinel nodes and how they are used
  * Stack ADT, methods (push/pop/peek), stack implementation (fixed length Arrays, ArrayLists, or LinkedLists), stack operations (must be able to describe/replicate symbol balancing, reversing symbols, post-fix expressions, etc)
  * Queue ADT, implementations, Josephus problem (probably not on exam, just review)
* chapter 4: through 4.4, read 4.6, maps (key/value pairing, definition, check in section 4.8), sets
  * generalized trees (0 or more children at each node)
  * first child/next sibling representation
  * tree traversals
  * Binary trees, be able to express an algorithm to build ExpressionTree for postfix expression
  * pre/post/infix traversals of trees and resultant expressions, must deal with parenthesis with infix expressions
  * reverse engineer a postfix/infix expression to build an ExpressionTree
  * BSTs, methods and runtimes, distinction between balanced BSTs, recursive/iterative methods on BSTs, full remove method, lazy deletion, AVL conditions and rotations, full/complete/perfect binary tree definitions
* chapter 5: through 5.3, hash tables, separate chaining
    * hash maps, tables, separate chaining, load factor, collisions, rehashing
* Tower of Hanoi problem as an example of exponential-cost recursion
* Josephus problem as an example of a queue

<Br>__Additional Details__
* tail recursion
