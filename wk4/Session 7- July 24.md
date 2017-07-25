# Data Structures - Session 7, July 24
* homework 3 is going to be split in half, with the programming portion being posted either today or tomorrow. There will be a separate submission date for homework 3's programming portion.
* midterm scores will be up anywhere from tomorrow to Thursday
* final will be cumulative, two of the questions from the midterm will show up on the final. Question 1 will be an induction proof on graphs. The AVL question may or may not be on the final. The final will be 50% longer than the midterm, with twice the amount of time.

<br>__Hashing - Open Addressing Schemes__
* not separate chaining, only one piece of data can go in a given slot. In a hash table with an open addressing scheme, the maximum load factor is 1. The target load factor will be 0.5, at which point, we will rehash.
* open addressing schemes are also known as probing the table. Probing the table for empty spots means looking for the next open spot and, if available, placing the data there. We will number the probes $h_i(x)$.
  * when doing these open addressing schemes, we will have a probing function. For example $h_i(x) = (hash(x)+f(i))$ % $TS$
* with a hash table, we'd want to be able to insert, remove, and see if a table contains a specific value for a particular key
* two major types of probing (with a third mentioned in the book)
  * linear probing - probing function is linear, linearly stepping through after the space until you find a valid (empty) space
    * primary clustering - the grouping of values close to a specific hash entry, allowing more and more collisions with later entries as the hash table gets more and more populated
    * with separate chaining, we're aiming for a load factor of 1
    * linear probing is prone to primary clustering within a couple of entries
    * to find a value for a contains check, we would run through the $h(i)$ function to check through the probes until we found the value or an empty space. The contains check will then have the possibility of stopping at an empty space, regardless of whether or not the value is right after it. The contains check will stay the same (regardless of whether or not we have a value in the space after the empty space). We will modify the remove method instead, implementing a lazy deletion-like technique and flagging a "deleted" value in its entry. This allows an invalid value to be skipped over during a search, or the flag to be removed if the same value is to be inserted at a later point.
    * lazily deleted elements are still factored into the load factor, since they still have to be probed through
    * an initial removal creates a lazy deletion, but a rehashing will force remove any lazily deleted elements
  * quadratic probing - $f(i) = i^2$, this means the $h_0$ probe is still the same, as is the $h_1$ probe. The changes come with $h_2$ probes and up.
    * since you're cycling through the hash entries in a non-linear pattern, it is possible that you might get stuck in a non-insertion loop within a non-prime sized table.
    * load factor must also stay below 0.5 for quadratic probing

    Say we have two probes, i & j, where $0 \leqslant i \space and \space j<TS/2$ and $i!=j$, with a prime TS
    $hash(x) + i^2$ = $hash(x) + j^2$ (mod TS)
    <br>$i^2 = j^2$ (mod TS)
    <br> $i^2 - j^2 = 0$ (mod TS)
    <br> $(i - j)(i + j) = 0$ (mod TS)
    <br> $(i-j)$ cannot be zero, since i is not equal to j
    <br> $(i+j)$ cannot be zero
    <br> but $(i -j)(i+j)$ cannot be true, since TS is prime.
  * double hashing - involves a second hash function, example: $f(i)*x$

* reading through section 5.4 and 5.5 (goes through rehashing)
* only going through section 6.3 on priority queues
* next week'll start sorting and graphs
