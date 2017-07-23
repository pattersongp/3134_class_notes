# Data Structures - Session 1, July 3

* midterm on Monday of week 4
* last Wednesday is the final
* four, maybe five assignments with the lowest one dropped
* 50% homework, 20% midterm, 30% on the final
* TA office hours in the evenings of Tuesdays, Thursdays, and Fridays

**Basic Data Structures**
  * an array is a data structure that contains a contiguous set of elements, where you only need to know the initial element location to find the entire structure
  * in an unsorted array, you would use linear/sequential search to find a specific element. This provides a worst case scenario Big-O(n).
  * in a sorted array, binary search could be used, where the initial value looked at is the midpoint and compared to the value being searched for. This cuts the array in half (if the searched value is greater or lesser than the midpoint value). In Java, integer division truncates, so the division between two integers would be another integer with the quotient favoring the lesser value. This provides a worst case scenario Big-O($logn$).
  * Binary search note: since it takes a single comparison to divide the number of comparisons by 2 in binary search, the number of comparisons it would take for $2^x$ comparisons to finish would be x, as $2^{x-x} = 2^0 = 1$. This means that the binary search Big-O(x) = Big-O(logn), since $2^x$ expressed in terms of $n$ would be equal to $logn$.
  * an ArrayList is a wrapper of an Array that allows you to use ArrayList methods to resize, change, and grow the array as needed.
  * a LinkedList has a node, the data you're trying to store in that node, and a reference to the next element in the list. ArrayList methods can still be used with LinkedLists, but might do different things when invoked on LinkedLists.

**Generic Identifier Example:**
``` java
  ArrayList<Integer> a = new ArrayList<>(); //creates an ArrayList of integers
  // a generic class is one that will work on any specified data type; in this example,
  // the ArrayList is a generic class
  // generics must be used with wrappers as they cannot be used with primitives
```

**Induction Proof Example:**
  1. $F_i < (5/3)^i$ with $i >= 1$
  2. $F(1) < (5/3)^1$: this is the base case, and is true
  3. Assume for i from 1 to some k that the above hypothesis is true. If the argument holds for the first k, then $(k + 1)$ must also hold.
  4. We need to actually prove that $F(k + 1) < (5/3)^{k + 1}$ is true.
  5. $F(k + 1) < (5/3)^k + (5/3)^{k - 1}$
  6. $F(k + 1) < (3/5)(5/3)^{k + 1} + (3/5)^2(5/3)^{k + 1}$: divide both summarands by the reciprocal to get the exponent to $(k + 1)$
  7. $F(k + 1) < (15/25)(5/3)^{k + 1} + (15/25)^2(5/3)^{k + 1}$
  8. $F(k + 1) < (24/25)(5/3)^{k + 1}$

**Recursive Methods**
* recursion is a function that is defined in terms of itself
* Fibonacci sequence: $Fib(k) = Fib(k - 1) + Fib(k - 2)$ with initial values of $Fib(0) = 1$ and $Fib(1) = 1$.
* Four Rules of Recursion
  1. there must be a base case
  2. with each call to the recursive method, there must be progress towards the base case
  3. the design rule - write your recursion assuming the recursive calls work
  4. don't repeat work - repeating work will make work accumulate exponentially. Keep track of the work that has already been done, aka "memoizing".

**Factorial example**
  ``` java
  public class Factorial {
    public static int factorial(int x) {
      // Base Case
      if (x==0) {
        return 1;
      }

      // Recursive call
      return x * factorial(x - 1);
    }
  }
  ```

**Fibonacci example:**
  ``` java
  public class Fib {
    public static int fib(int x) {
      // Base case
	  	if (x == 0 || x == 1) {
		  return 1;
  		}

      // Recursive call
	  	return fib(x - 1) + fib(x - 2);
	  	}
  	}

	  public static final void main(String[] args) {
	  	int x = Integer.parseInt(args[0]);
	  	System.out.println(fib(x));
  }

  // looking for the nth Fibonacci number turns this algorithm's complexity into Big-O(2^n)
  // since each call splits the complexity by another factor of 2. This leads to
  // unreasonable costs at larger integers.
  ```
* class generics - generics like ArrayLists, where data type is defined upon use
* method generics - method that works on any input; using generics allows the data type to be bound to a certain type. Comparable interface uses the class generic as the data type is defined once and is used the same throughout the rest of the interface.
* invoking binary search on a set of objects may or may not require the Comparable interface to allow the elements to be arranged in an array
* BinarySearchGenerics example:
  - invoking BinarySearchGenerics will infer the data type, i.e. AnyType was supposed to be a Person type object
  - recursive driver method - a public driver method that isn't recursive bootstraps a private recursive method
* BinarySearchGenerics: extending comparable, where does the compareTo method get defined?
