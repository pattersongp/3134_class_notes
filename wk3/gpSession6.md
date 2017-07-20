#Data Structures and Algorithms
July 19, 2017

#Table of Contents
1. [Admin](#admin)
2. [AVL Trees](#avl-trees)
3. [Hashing](#hashing)

##Admin
* Homework 1 solution on courseworks
* Homework 3 you need to know something about the instance variables for the problem about 2 stacks in 1 array. You should write some psuedocode for this and make it verbose
* 

##Midterm

###Questions
* Given a list of numbers/comparables, insert them into an initially empty AVL tree, showing all rotations, etc
* The midterm goes up to and includes seperate chaining, everything before seperate chaining
* at 530PM on Monday
* 6-7 problems on the exam, with multiple problems. The 7th question will be on hash tables
* Mixture of short answer questions
* Algorithm, big-oh cost, given some algorithm, whats hte big-oh cost?
* 1st Question of the test will be an induction proof, it will be about trees
* chances are you'll have to do something with a recursive method for doing something with a tree
* Questions
	1. inductive proof on basic property of binary tree
	2. tree algorithms by hand
	3. AVL tree
	4. Big-Oh Cost
	5. 
	6. 
	7. HashTables

###Readings
- Chapter 1, generics, recursion, induction proofs
- Chapter 2, entire thing, expect 2.4-3
- Chapter 3, Pretty much whole thing, all lists
- Chapter 4, 4.4, 4.6
- Chapter 5, 5-5.3

###From Class
- Tower of Hanoi (exponential time)
- Josephis Problem (queues)

###The Comprehensive list for the test
- basic proofs, recursion and the rules of recursion, generics, nested classes (differences between static and nonstatic)
- big-oh notation know the definitions of big-theta, big-omega, big-oh, worst-best-average case analyses, various techniques of analyzing algorithms, if statements and big-oh, recursive big-oh, Knowing what is faster than anything else,
- know what the list abstract data type is, knowing the particular runtimes of inserts, removes, running out of space in the arrays, singly and doubly linked lists, adding and removing elements from a linkedList, stack ADT and all of its methods, Knowing applications of stacks in general especially building post-fix expressions using stacks, queue ADT both array and stacks etc
- Generalized trees not restricted to anything, recursive definitions of tree traversal, visiting every node of a generalized trees, construction of expression trees, building an expression tree from a post fix expression, pre-post-in order traversals, If I gave you the in-order traversal and pre-fix expression -- can you give me the original tree?, binary search trees, runtimes of methods on binary searchtrees, definitions of binary search trees, writing methods on BST's, lazy deletion, AVL tree condition, performing rotations, complete full perfect binary trees
- rehashing, load factor, rehashing, separate chaining
- tail recursion?

##AVL Trees
*

```Java
    // Assume t is either balanced or within one of being balanced
    private AvlNode<AnyType> balance( AvlNode<AnyType> t )
    {
        if( t == null )
            return t;
        
        if( height( t.left ) - height( t.right ) > ALLOWED_IMBALANCE ) // will always be 2
            if( height( t.left.left ) >= height( t.left.right ) )
                // left left                // left right
                // zig zig                  // zig zag
                t = rotateWithLeftChild( t );
            else
                t = doubleWithLeftChild( t );
        else
        if( height( t.right ) - height( t.left ) > ALLOWED_IMBALANCE ) // will always be zero
            if( height( t.right.right ) >= height( t.right.left ) )
                // right right              // right left
                // zag zag                  // zag zig
                t = rotateWithRightChild( t );
            else
                t = doubleWithRightChild( t );

        t.height = Math.max( height( t.left ), height( t.right ) ) + 1;
        return t;
    }

    private AvlNode<AnyType> rotateWithLeftChild( AvlNode<AnyType> k2 )
    {
        // this is the single rotation
        ////////////////////////////////
        AvlNode<AnyType> k1 = k2.left;
        k2.left = k1.right;
        k1.right = k2;
        ////////////////////////////////
        k2.height = Math.max( height( k2.left ), height( k2.right ) ) + 1;
        k1.height = Math.max( height( k1.left ), k2.height ) + 1;
        return k1;
    }
```

##Hashing
* What is a hash table?
	* A table of values corresponding to the pre-image of some hash function, modded by the size of the hash table
	* Good table sizes are prime, because you're less likely to have collisions and 
* What is a hash value?
	* You take some sort of data, then you apply a mathematical function that gives you a value, the hope is that whatever function you're using is a 1-to-1 function, because that hash needs to be unique
	* Good hashing functions do not have an inverse, but this is not required for a hash function
* Once you have a hash value, you're supposed to mod % the value by the size of the table
* How do we handle hash value collisions?
	* We can add a 1 to the value
	* We can also use separate chaining. We can use N-D ArrayLists and LinkedLists to represent our hash-table
* Load Factor (Lambda) the ratio of number of elements in the table, to the size of the table.
	* If you keep your lamba to a seperate chaining hash-table to 1 or lower, you're guarenteed to have lengths on average of 2-3
	* When we have a lambda above one, we use a technique called rehashing, we use the value, then go through the process of hashing again
* 

##Maps
* A set of key value pairs where each key maps to a specific value
* Maps in java have 2 generics 
* Interface