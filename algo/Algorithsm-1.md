Algorithsm
----------

30.1 Introduction
Insidious bug
Quadratic
Caveat

30.2 Data structure
Stack
Linked list implementation for stack.


Proposition. Every operation takes constant time in the worst case.
Proposition. A stack with n items uses ~ 40 n bytes.
Remark. This accounts for the memory for the stack
(but not memory for the strings themselves, which the client owns).


Array implementation for Stack



Resizing array
􀉾 push(): double size of array s[] when array is full.
􀉾 pop(): halve size of array s[] when array is one-quarter full.

Linked-list implementation.
􀉾Every operation takes constant time in the worst case.
􀉾Uses extra time and space to deal with the links.
Resizing-array implementation.
􀉾Every operation takes constant amortized time.
􀉾Less wasted space.


Queue




Job interview problem. Implement a queue with two stacks so that:
􀉾Each queue op uses a constant amortized number of stack ops.
􀉾At most constant extra memory (besides the two stacks).
Solution. Call the two stacks incoming and outgoing.
􀉾enqueue: push to incoming
􀉾dequeue: pop from outgoing
– if outgoing is empty, first “pour” incoming into outgoing (O(N)).
􀉾isEmpty: check if both stacks are empty

Genercs

Iterator
Java: for-each loop

For a user-defined collection, do this to enable looping over it with for-each:
􀉾Data type must have a method named iterator().
􀉾The iterator() method returns an object that has two core methods.
– the hasNext() methods returns false when there are no more items
– the next() method returns the next item in the collection
Iterator interface: next() and hasNext() methods.
􀉾 Iterable interface: iterator() method that returns an Iterator.

Concurrent modification: ConcurrentModificationException.


Arithmetic expression evaluation based on two stacks

























Common mistake. Interpreting big-Oh as an approximate model.


30.3 Sort
Selection sort






Insertion sort



Proposition. For partially-sorted arrays, insertion sort runs in linear time.
Pf. Number of exchanges equals the number of inversions.
Binary insertion sort. Use binary search to find insertion point.
􀉾Number of compares ~ N lg N .
􀉾But still a quadratic number of array accesses.
Client object must implement an interface (comparable).
Comparable -> compareTo().
Comparator -> compare()

Arrays.sort(a, String.CASE_INSENSITIVE_ORDER)

Knuth shuffling
􀉾In iteration i, pick integer r between 0 and i uniformly at random.
􀉾Swap a[i] and a[r].

Merge sort






A sorting algorithm is in-place if it uses ≤c log N extra memory.


Uses too much overhead memory for small arrays
private static void sort(Comparable[] a, Comparable[] aux, int lo, int hi)
{
if (hi <= lo + CUTOFF - 1)
{
Insertion.sort(a, lo, hi);
return;
}
int mid = lo + (hi - lo) / 2;
sort (a, aux, lo, mid);
sort (a, aux, mid+1, hi);
merge(a, aux, lo, mid, hi);
}

Bottom-up merge sort
public class MergeBU
{
private static void merge(...)
{ /* as before */ }
public static void sort(Comparable[] a)
{
int N = a.length;
Comparable[] aux = new Comparable[N];
for (int sz = 1; sz < N; sz = sz+sz)
for (int lo = 0; lo < N-sz; lo += sz+sz)
merge(a, aux, lo, lo+sz-1, Math.min(lo+sz+sz-1, N-1));
}
}

Timsort
Natural mergesort.
􀉾Use binary insertion sort to make initial runs (if needed).
􀉾A few more clever optimizations.


Quicksort
private static int partition(Comparable[] a, int lo, int hi)
{
int i = lo, j = hi+1;
while (true)
{
while (less(a[++i], a[lo]))
if (i == hi) break;
while (less(a[lo], a[--j]))
if (j == lo) break;
if (i >= j) break;
exch(a, i, j);
}
exch(a, lo, j);
return j;
}

public class Quick
{
private static int partition(Comparable[] a, int lo, int hi)
{ /* see previous slide */ }
public static void sort(Comparable[] a)
{
StdRandom.shuffle(a);
sort(a, 0, a.length - 1);
}
private static void sort(Comparable[] a, int lo, int hi)
{
if (hi <= lo) return;
int j = partition(a, lo, hi);
sort(a, lo, j-1);
sort(a, j+1, hi);
}
}
Quicksort is a randomized algorithm.
􀉾Guaranteed to be correct.
􀉾Running time depends on random shuffle.
Expected number of compares is ~ 1.39 N lg N.

Selection
Find the kth smallest key
public static Comparable select(Comparable[] a, int k)
{
StdRandom.shuffle(a);
int lo = 0, hi = a.length - 1;
while (hi > lo)
{
int j = partition(a, lo, hi);
if (j < k) lo = j + 1;
else if (j > k) hi = j - 1;
else return a[k];
}
return a[k];
}

Quick-select takes expected linear time.

Arrays.sort()
􀉾Dual-pivot quicksort for primitive types.
􀉾Timsort for reference types.

30.4 Priority queue
Binary heap
public class MaxPQ<Key extends Comparable<Key>>
{
private Key[] pq;
private int N;
public MaxPQ(int capacity)
{ pq = (Key[]) new Comparable[capacity+1]; }
public boolean isEmpty()
{ return N == 0; }
public void insert(Key key) // see previous code
public Key delMax() // see previous code
private void swim(int k) // see previous code
private void sink(int k) // see previous code
private boolean less(int i, int j)
{ return pq[i].compareTo(pq[j]) < 0; }
private void exch(int i, int j)
{ Key t = pq[i]; pq[i] = pq[j]; pq[j] = t; }
}

Heap sort
public class Heap
{
public static void sort(Comparable[] a)
{
int N = a.length;
for (int k = N/2; k >= 1; k--)
sink(a, k, N);
while (N > 1)
{
exch(a, 1, N);
sink(a, 1, --N);
}
}
private static void sink(Comparable[] a, int k, int N)
{ /* as before */ }
private static boolean less(Comparable[] a, int i, int j)
{ /* as before */ }
private static void exch(Object[] a, int i, int j)
{ /* as before */ }
}

冒泡, selection, insertion, shellsort
mergesort, bottom-up mergesort
quicksort, quick-select (the kth element), 3-way quicksort
priority queue, binary heap, heapsort
binary search in array, find min/max
binary search tree, put, floor, count->rank; in order tranversal, delete
2-3 tree, red-black tree, B-tree








HashTable




Java system includes both.
・Red-black BSTs: java.util.TreeMap, java.util.TreeSet.
・Hash tables: java.util.HashMap, java.util.IdentityHashMap.

Str.split(“\\s+”): split by blank space!!

Sparse matrix-vector multiplication
Problem. Sparse matrix-vector multiplication.
Assumptions. Matrix dimension is 10,000; average nonzeros per row ~ 10.
