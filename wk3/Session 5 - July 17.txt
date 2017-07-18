# Data Structures - Session 5, July 17
* chapter 5.1 to 5.3 at the latest on Wednesday
* homework 1 solutions will be released within the day
* midterm will take half the class on Monday with lecture afterwards; closed book, closed notes
* one midterm question will be an inductive proof on the properties on BSTs. Other questions might include inserts, etc.

<br>__Homework__
* last written problem on HW2, should explain the pattern of the unsolvable sequence
* temp variable can be used for the singly linked list rearrangement
* java-like pseudocode for LinkedList problems, no paragraphs

<br>__Expression Tree Class__
* not generic, as each node has a specific data type attached to it
* ExpressionTree class preview
  ``` java
  public class ExpressionTree{
    public ExpressionTree(String expression) {
      // here we write our stack based method
      // for building an expression tree.
      // when we pop off the final node after
      // processing all tokens, set root equal to that node
    }

    // must write a prefix, infix, postfix, and eval method

    public int eval() { // public driver method
      return eval(root); // private recursive method
    }

    private int eval(Node t) {
      // recursive algorithm goes here
    }

    // does not need access to outer variables, thus is static
    private static class Node {
      Node left;
      Node right;
      char operator;
      int operand;
      boolean isOperator;
    }

    Node root = null;

  }
  ```

* Tester class preview
  ``` java
  public class ExpressionTester {
    public static final void main(String[] args) {
      ExpressionTree = new ExpressionTree("35 6 2 + -");
      System.out.println(tree.eval()); // should print out the correct answer
    }
  }
  ```
* do not push ExpressionTrees onto the stack, push Nodes

__Binary Trees__
* Example: proof by induction
  * if we have a binary tree of height $h$, the number of leaves is at most $2^h$
  * base case: for h = 0, $2^0 = 1$, base case holds
  * assume that all perfect binary trees of height $n$, where $n$ goes from $0$ to an arbitrary $h$, have $2^h$ leaves
  * assume two perfect binary trees of height $h$, and $2^h$ leaves: creating a root to connect both of these at the top would construct a perfect binary tree of $h+1$
  * the total amount of leaves would be $2^h + 2^h = 2*2^h = 2^{h+1}$
* Example:
  * total nodes in perfect binary tree of height h is $2^{h+1} - 1$
  * base case: $h = 0, 2^{0+1}-1=2-1=1$, base case holds
  * assume true for heights $0$ to $h$
  * prove $h+1$ means number of nodes is $2^{h+2}-1$
  * adding a common root node to the top of two perfect binary trees creates a tree with $2^{h+1}-1+2^{h+1}-1+1$
  * this solves to be $2^{h+2}-1$

<br>__Binary Search Trees (BST)__
* BST condition is a constraint on what kind of data can be on the left and the right of a node
* any nodes in the left subtree must be smaller than the node itself, any nodes in the right subtree must be larger than itself
* in this case, there will be no duplicate values. BSTs are a type of set, where sets do not have any duplicate values
* there can be valid Binary Search subtrees based on the rooting reference
* both insert and search methods would run recursively through the nodes to place or insert the value, respectively
* the worst case runtime of the BST is the height of the tree; if the BST degenerates into a LinkedList, the furthest leaf would be the fulle $n$. This would mean the cost of a search/insert method on a BST would be $O(n)$.
* Example: degenerate BST
  * taking in a sequence 1, 3, 5, 7 with a root node of 1 would result in a BST that results in a LinkedList.
  * inserting the sequence in reverse order would result in the same LinkedList, just in a different order
* findMin method - would keep advancing to the left until null is hit; findMax would be the opposite way until null
* remove method - includes search operation (must find before removing)
  * a node without children can just be removed
  * a node with one child can be removed and replaced with its child, as the child's subtree will properly fit in their new place
  * a node with two children is more difficult to remove; the replacement node would be the largest node in the left subtree (as its larger than everything in the left) or the smallest node in the right subtree (as its smaller than everything else in the right)
* lazy deletion is when you don't actually want to delete a node. For example, you add a boolean data type in the nodes; where true would indicate it being present in the tree and false meaning it's marked for deletion and its not actively part of the tree. Insert/remove would just switch this boolean back and forth between true/false.
  * findMin and findMax would have to also double check this boolean, as it wouldn't be as simple as traversing down the left/right side of the tree. These methods would not be able to be written as loops, only as recursion.

<br>__Self-Balancing BSTs and AVL trees__
* insert operations also adjust the organization of all the nodes so that everything is continually on the order of O(logn) costs
* AVL trees are named after Adelson-Velsky and Landis; they are a type of self-balancing BST
  * AVL trees have two conditions, the BST condition and the AVL condition, which is also known as the so-called balance condition
  * the balance condition says that at any node in the tree, the height of its left subtree cannot differ from the height of its right subtree by more than one
  * Example: a single root node would be a valid AVL tree, since it is larger than both left and right subtrees. The balance condition is upheld correctly as well, since the height of both left and right subtrees is -1.
  * add data to nodes that add their heights to the nodes. This spares us the cost of calculating the heights through each run.
* Four categories of imbalance in a BST:
  * Case 1: going left twice (zigzig case)
    * can be solved by a single rotation between the left child and the root to change the root and balance the tree
  * Case 2: going left, then right down a single node (zigzag case)
    * the third element in the chain will be the new root, requiring a double rotation. The third element will switch with the second element as the first rotation. The second rotation will follow the zigzig case single rotation.
  * Case 3: mirror case: going right twice (zagzag case)
    * can be solved by a single rotation between the right child and the root to change the root and balance the tree
  * Case 4: mirror case: going right, then left down a single node (zagzig case)
    * mirror the zigzag double rotation
