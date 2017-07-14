#Data Structures and Algorithms
**July 12, 2017**

##Admin
* README should have the files that you're submitting
* make sure to put your name on it

##Postfix expression
* enter the operand first, then the operator
	- 3 5 +
* these are useful becaues we can express something like: 3 * (2+5) but we can write this without parantheses as: 3 5 2 + *
* we can express this in an algorithm
* Turnary operator: `operand ? operand : operand`, this is a one-liner for doing if-else conditional statements
* Note that for these, we can actually mix operators
	- we can write: 5 2 - 3 * or 3 5 2 - * which is the same thing

###Psuedocode for execution postfix expressions
1. read in the expression
	- if the item read is an operand, push it to the stack
2. once you hit an operator, pop 2 items from the stack (being careful to put the first item to the right, then second to the left)
3. push the result of the first popped expression back onto the stack
4. if you scan another operator, pop 2 items from the stack and execute line 2 again.
	- if there isn't 2 items, the expression was incomplete throw an error
	- if you have no more operators to scan and the stack isn't empty, throw an error

##Queues
* Often referred to as FIFO, first in first out
* What should we have for the ADT?
	- `size()`
	- `isEmpty()`
	- `enqueue(someElement)`
	- `dequeue(someElement)`

* we can enqueue items from the back, then we'll dequeue things from the front. When we hit the end of array, because we're bound to hit the end of the array. We can increment it by 1, then mod `%` the tail by length of the array.
	- this occurs whenever we want to wrap the head or tail pointer back to the front of the array
* Keep a variable that tracks the size, then whenever the we want to add something to pushes the size above the length of the array, then we just grow the array with some tricky interation
* we can use a doubly linked list to guarentee an always order of 1, constant time

```Java
import java.util.LinkedList;
import java.util.Queue;

public class Josephus {
	public static find void main(String[] args) {
		int count = 5;
		Queue<Integer> q = new LinkedList<Integer>();

		// fill up the queue
		for (int i =1; i<10; i++) {
			q.offer(i); // example of autoboxing
		}

		int currentCount = 0;

		while (q.size() != 1) {
			int x = q.poll() // dequeue
			currentCount++;

			if (currentCount == 5) {
				System.out.println("Kill: " + x);
			} else {
				q.offer(x);
			}
		}
		int winner = q.poll();

		System.out.println("The winner is: " + winner);
	}
}
```

##Trees
They can be, often are, defined recursively
* Trees have:
	- a root
	- interior nodes
	- subtrees
	- leaves
	- pathes
	- levels
* Linked Lists are degenerate trees
* Nodes have
	- children
	- parents
	- depth : the length in edges of the unique path back to the root, the depth of the root is 0
	- height : the length in edges  of the path from a given node to the furthest leaf
* its useful to think about the height of an empty tree as `-1`

###Representations of trees in Java
```Java
// The Generalized Tree
public Tree<AnyType>{
	AnyType data;
	TreeNode<AnyType> nextSibling; // we use this only in the data structure
	TreeNode<AnyType> firstChild;
}
```
###Tree Traversals
####Preorder Traversal
* Executes work at node first
* Then traverses all the children

####Postorder Traversal
* Executes work at children first
* Then returns to the node to do the work

##Binary Trees
A tree where each node either has 0, 1, or 2 children. We can describe them as  `leftChild` and `rightChild`.
* A binary tree is called **full** IFF every node has either 2 children or is a leaf
* A binary tree is called **complete** IFF every level in the tree is completely filled in, except the the last level, which must be filled in from left --> right
* A binary tree is called **perfect** IFF every level in the tree is completely filled in
```Java
public BinaryNode<AnyType> {
	AnyType data;
	BinaryNode leftChild;
	BinaryNode rightChild;
}
###Use Case for Binary Tree
Expression Tree

```Java
int eval(ETNode t) {
	if(t.isOperand) { return t.value; }
	int leftVal = eval(t.left);
	int rightval = eval(t.right);
	return apply(t.operator, leftVal, rightVal);
}
```
* Note that given some expression tree, if you perform a postfix traversal on the tree, you'll get a postfix expression

####In-order Traversal
this will given you an expression that we're used to seeing like 1 + (4*2). Before you recurse on any subtree, you need to print an `(` then after any subtree print `)`

1. recurse left
2. print node
3. recurse right

###Building an expression tree
Given some post-fix expression, build an expression tree
* Given: 4 3 2 + *
* Use a stack to build an expression tree
####Algorithm for building the tree
1. start at 0, put that data into an expression node
	- if that node's data is an operand, push it onto the stack
2. continue with line 1 until you reach an **operator**
3. If operator, make a node for it
	- pop the stack once and make that value the right subtree of that node
4. Push that operator node back onto the stack, the children come along because they're still pointing at the stack
5. repeat until the the expression is either empty or you end up with another operand
6. if the expression is empty, pop the stack and thats the tree
7. check that the stack is empty, if not --> something went wrong