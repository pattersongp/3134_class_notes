# Data Structures - Session 4, July 12
* homework 2 will be based on chapter 3/4, will be released either later today or tomorrow night
* homework 5 will NOT be due on the Thursday after the final exam, rather the Tuesday before it
* read through 4.3 and start reading 4.4 for the next class
* will be shifting to a Thursday to Thursday homework cycle
* __provide dimensions in rectangle output for binarySearch__

<br>__Stacks, Continued__
* reverse Polish notation, also known as post-fix notation, is where operands come before operators
  ```
  postfix example: 3 5 +
  infix example: 3 + 5

  infix example: (3 + 5) * 2
  postfix example: 3 5 2 + *
  ```
* reverse Polish notation uses stack operations

<br>__Stack Example__
   ```
   3 5 2 + *
   ```
   * the first three tokens are operands, followed by an operator
   * when the algorithm reaches the first operator, it pops twice (pulling 2 and 5) and applies the first operator between them to get 5 + 2 = 7
   * this 7 is then pushed back onto the stack
   * popping an empy stack (i.e. receiving an operator before pushing two operands) will cause a stack underflow
   * the next token will be an operator, which will make the algorithm pop twice, apply the operator between them to get 3 * 7 = 21
   * error conditions include checking the stack to make sure its empty and ensuring there are two operands in the stack
   ```
   5 2 - 3 *
   3 5 2 - *
   These will result in the same answer
   ```

<br>__Queue Abstract Data Type__
* FIFO, First-In-First-Out data structure
* much like a stack, we should have a size, isEmpty, isFull
* two main methods are enqueue (adds elements) and dequeue (removes elements)
* using an array, we would enqueue elements at the tail end and dequeue at the front end (idx: 0) of the array
  * dequeueing an item would require the head index to shift up one to allow the previous item to be removed
  * alternating enqueueing and dequeueing would eventually lead us to the end of the array--this is where we use modulus operations to allow a wraparound function. We would increment the head and tail markers before modding by the array size to allow the proper wraparound place
  * we would also use a variable to keep track of the size of the queue to ensure we don't try to enqueue anymore items
* using a doubly linked list would allow us to enqueue at one end and dequeue at the other end without any hassle, at Big-O(1) runtime
* using a singly linked list would create Big-O(n) runtime, so we would never use a singly linked list for queues

<br>__LinkedList__
* the add and remove methods for a LinkedList do so at opposite ends, making a LinkedList effectively a queue
* LinkedLists also have methods to push and pop for stack functionality
* offer and poll are also alternative names that can be used in lieu of enqueue and dequeue

<br>__Josephus Problem__
  ``` java
  import java.util.LinkedList;
  import java.util.Queue;

  public class Josephus {

    public static final void main(String[] args) {the node

      int count = 5;
      // the queue is an interface that cannot be instantiated
      // so we instantiate using LinkedList
      Queue<Integer> q = new LinkedList<Integer();

      for (int i = 1;i<=10;i++)
        q.offer(i);

      int c = 0;

      while (q.size() != 1) {
        int x = q.poll();
        c++;
        if (c == 5) {
          system.out.println("So long: " + x)
          c = 0;
        } else {
          q.offer(x);
        }
      }

    }

    System.out.println("The winner is: " + q.poll());

  }
  ```

<br>__Trees__
* trees can be defined recursively, they also have root nodes
* root nodes have zero or more subtrees hanging off of them, which are trees as well
* a LinkedList is a tree, where each node in the tree is allowed to have zero or one nodes hanging off of it
* the top level node is called the root, the nodes hanging off of a tree are called children, or child nodes
  * the parent nodes are above the child nodes
  * nodes that are children of the same parent are considered siblings
  * nodes that have no children are referred to as leaf nodes, or leaves
  * nodes that are not leaves are interior nodes, including the root node
  * in a path, you can only move from a root to a child
  * the depth of a node is the length of the unique path back to the root; the depth of the root is zero
  * the height of a node is the length of the path from a given node to the furthest leaf
  * a tree with a single root node would be called an empty tree, with a height of -1

<br>__TreeNode Example__
  ``` java
  class TreeNode<E> {
    E data;
    TreeNode<E> nextSibling;
    TreeNode<E> firstChild;
  }
  ```
  * firstChild will link to the first following child of the root
  * nextSibling will link the first child to the next child node

<br>__Tree Traversal/File Directory Example__
* a pre-order traversal prints the node first, then it prints the children
* post-order traversal is simply in reverse

<br>__Binary Tree__
* a tree where every node is restricted to having zero, one, or two children
* the child nodes are known as the left child and the right child
  ``` java
  class BTNode<E> {
    E data;
    BTNode<E> left;
    BTNode<E> right;
  }
  ```
* full - every node has either two children or is a leaf
* complete binary tree - a binary tree where every level is completely filled in, except for the last level, which must be filled in from left to right
* perfect binary tree - a binary tree every level is fully filled in, is also complete

<br>__Expression Tree__
* takes a mathematical expression and represents it in tree form
* each node in the expression tree can be one of two types: an operator or an operand
* operand nodes are leaves, operator nodes have operand children
  ``` java
  int eval(ETNode t) {
    if (t.isOperand)
      return t.value
      int lval = eval(t.left); // evaluates left child
      int rval = eval(t.right); // evaluates right child
      return apply(t.operator, lval, rval); // takes in an operator and two operands and applies the equation
  }
  ```
* a postorder traversal on an expression tree will result in a post-fix expression
* an inorder traversal is where the recursion starts to the left, printing as it makes its way to recurse to the right, resulting in an in-fix expression
  * before recursing on a subtree, print an open parenthesis
  * before leaving the subtree, print a closed parenthesis
* a preorder traversal works at the node first and creates pre-fixed expressions

<br>__Expression Class__
* constructor for Expression class will take a postfix expression and creates an expression tree
  ```
  4 3 2 + *
  ```
  * create a stack of ExpressionNodes
  * push the operands onto the stack (4, 3, 2)
  * create a node around the first operator and pop the stack once to create its ight subtree (2)
  * pop the stack again to create its left subtree (3)
  * push the operator node onto the stack (+)
  * moving to the next token (*), create an ExpressionNode around the operator
  * pop the stack twice, for the right subtree (+) and the second for the left (4)
  * push the single node onto the stack, check for another token
  * since there are no tokens left, pop the stack for the answer, check the stack.isEmpty to verify
