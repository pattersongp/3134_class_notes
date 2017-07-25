#Data Structures In Class Notes
**July 17 2017**

# Table of Contents
1. [Admin](#admin)
2. [ExpressionTrees](#expressiontree-continued)
3. [Binary Trees](#binary-search-tree)
4. [Balanced BST's](#self-balancing-binary-search-trees)

##Admin
*Midterm half the class
*write all psuedo-code in Java-like code
*Midterm guide review posted on Wednesday
*Midterm will have an induction proof on the properties of binary search trees
*Study how to write an insert element into a tree

##ExpressionTree Continued
*Not Generic at all, each node has specific data-types associated with it
*Nodes are internal to the ExpressionTree class ie nested
**Expression Tree Class Example**
```Java
public class ExpressionTree {
	
	private static class Node {

		Node left;
		Node right;
		char operator;
		int operand;
		boolean isOperator;
	}

	//ExpressionTreeClass Start

	Node root; //All other nodes will hang off that root
	public ExpressionTree(String expression){
		//populate Expression tree here

	}
	public int eval() {
		// takes in nothing
		// calls a recursive in-order tree traversal
		return eval(root);
	}
	private int eval (Node t) {
		//recursive method here
	}
}
```

##Binary Trees

###Proof for number of Leaves
If you have a binary-tree of height _h_, I want to be able to say how many leaf nodes there are. The number of leaves in a binary-tree is **at most** 2^h. The perfect binary-tree of height _h_ will have 2^h leaves.
1. We see that the base case is of height 0, then the 2^0 perfect binary-tree has 1 leaf. So the base case holds true.
2. Assume that all perfect binary trees of height _n_ where _n_ goes from 0 to _h_ have 2^n leaves.
3. Then it follows that height _h+1_ needs to have 2^{h+1} leaves
4. Then with 2 perfect binary trees with 2^h leaves, then adding a root which connects both of them, then you can add them together. You'll have 2^h + 2^h = 2 * 2^h = 2^{h+1}

###Proof for number of Nodes
We want to prove total nodes in a perfect binary tree of height h is **2^{h+1} - 1**. The height is a binary tree is log_(n) where n is the number of nodes
1. base case: h = 0, 2^1 - 1 = 1
2. Assume true for heights 0 to h, then we want to prove true for height h+1 is 2^{h+2} - 1
3. Then we can build two perfect binary trees of 2^{h+1}-1, then adding them both together, then + 1 for the new root node that we've added, we end up with **2^{h+2} - 1**

###Binary Search Trees - BST's
*The Binary Search condition is a constraint that defines what can be on the left and right of any given node. The binary search node has data that has to be comparable. Any node in the left subtree of a node, must be less than the parenting node. Then it follows that any right subtree will be greater than the parenting node's data. That is all nodes on the left and right of any given Node.
####Inserting and Searching
*The worst case is that you have to go to the bottom of the tree, which is the height _h_ of the tree.
*The worst case is that you have a big-oh of N cost, because there are situations when you degenerate into a linked-list
	- this would occur is something like: 1, 2, 3, 4 then inserting 1, then 2 ... You'll end up with a binary search tree that is actually shaped like a LinkedList

####Remove Operations
*You start by searching for it, if the target node has no children, then the operation is easy.
*If the target node has only 1 child, then its still very easy, you can just bring up that one child to the position of the targeted node
*If they have two children, the largest node in the left subtree, or the smallest node in the right subtree are the only ones that can replace the root of any tree or subtree

####BinarySearchTree Example
* Notice that for this one, you're **not** returning you're using the assignment operator.
```Java
private BinaryNode<AnyType> insert( AnyType x, BinaryNode<AnyType> t )
    {
        if( t == null )
            return new BinaryNode<>( x, null, null );
        
        int compareResult = x.compareTo( t.element );
            
        if( compareResult < 0 )
            t.left = insert( x, t.left ); // notice that you're assigning here, not returning
        else if( compareResult > 0 )
            t.right = insert( x, t.right );
        else
            ;  // Duplicate; do nothing // this is a pass call
        return t;
    }
```

#####In-Order Traversal Exmaple
*Prints in sorted order
*
```Java
private void printTree( BinaryNode<AnyType> t )
    {
        if( t != null )
        {
            printTree( t.left );
            System.out.println( t.element );
            printTree( t.right );
        }
    }
```

#####Remove Method
```Java
    private BinaryNode<AnyType> remove( AnyType x, BinaryNode<AnyType> t )
    {
        if( t == null )
            return t;   // Item not found; do nothing
            
        int compareResult = x.compareTo( t.element );
            
        if( compareResult < 0 )
            t.left = remove( x, t.left );
        else if( compareResult > 0 )
            t.right = remove( x, t.right );
        //The below only occurs if we're at the node that we want to remove
        //The above exactly the same as the insert method
        else if( t.left != null && t.right != null ) // Two children
        {
            t.element = findMin( t.right ).element;
            t.right = remove( t.element, t.right );
        }
        else
            t = ( t.left != null ) ? t.left : t.right;
        return t;
    }
```

####Lazy Deletetion
*We can do this with a boolean variable for ``Active``
*

##Self-balancing Binary Search Trees
A red-black trees are common balanced BST's, but we're going to go over AVL tree. These are self-Balancing binary search trees. So that means that the properties of a BST, plus two conditions. The **AVL condition** is the so-called balance condition, at any node in the tree, the height of its left subtree cannot differ from the right subtree by more than 1. This is where it is useful to think of the height of an empty tree as -1. You'll want to store the height of a node in the node itself. 
###Rotations
####We can group in 4 categories
1. 3 nodes going left, like a linkedList (zig-zig case)
	- calls for a single rotation
	- you want to make the left child the root of the tree in this case,
	- x -> y -> z because z <- y -> x
2. 3 nodes, 1 goes left, then right (zig-zag case)
	- this requires a double rotation
	- z will ultimately become the root
	- we single-rotate the bottom node, which gives us a zig-zig case then we can just do a single-rotation again
	- 
3. Then the mirror of 1
4. Then the mirror of 2

