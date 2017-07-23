# Data Structures - Session 3, July 10

__Stack Abstract Data Type__
* stacking up dishes, add/remove from the top
* the purpose of the stack is to allow us to add/remove elements from the top
* there are a set of methods that one typically provides for a stack
  * push - elements are pushed to a stack when they are added
  * pop - removing something from the stack
  * peek/top - looking at the top element of the stack
  * isEmpty
  * size
* stack is referred to as a "Last In, First Out", or LIFO, data structure
* anything that supports list operations can be used to make stacks
* arrays can be used as well, but then isFull() becomes important, as arrays have fixed sizes
  * using arrays would require us to use the end as the "top", since adding elements to the beginning of the array would require subsequent elements to shift towards the end
  ``` java
  a[theSize++] = x // push function
  return a[--theSize] // pull function
  ```
* using a singly linked list could provide Big-O(1) time, as long as you add at the front
* using a doubly linked list could provide Big-O(1) time from either beginning or end markers

__Stack Application, Bracket Checking Algorithm__
``` java
class a{
  public static main(String[] args) {
    System.out.println("why?");
  }
}
// anytime we see a character that isn't an open/close bracket, we ignore it
// anytime we see a character that is, we push it onto the stack
// anytime we see a closing bracket, we pop the stack to verify it matches and move on
// at the end of the file, we check that the stack isEmpty()
```
* can also be used to method calls, palindrome checking, reversing data (pushes on and pops off in reverse order)
