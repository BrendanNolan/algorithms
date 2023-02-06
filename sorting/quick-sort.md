# Quicksort

## Partition

The _Partition_ operation takes an array $A$, rearranges it, and returns an index $q$ such that
$A[q]$ is $\geq$ everything that comes before it and $\leq$ everything that comes after it. How it
works:

- Select the final element of the array as the _pivot_
- Imagine a contiguous selection (let us call it a _window_) of elements of the array, starting at
  the left and empty at first, containing elements $>=$ _pivot_. As you move left to right through
  the array, the window will always be immediately to the left of the element which you are
  considering.
- Moving left to right through the array (but stopping before the final element), if you hit an
  element $x$ which is $<=$ _pivot_, then swap $x$ with the leftmost element of the window - the
  effect will be to shunt the whole window over $x$ (and to move the leftmost element of the window
  to be the rightmost element of the window).
- When you reach the final element (pivot) of the array, swap it with the leftmost element of the
  window.

## Quicksort

```python
def quicksort(A):
    pivot = Partition(A)
    quicksort(A[0, pivot - 1])
    quicksort(A[pivot + 1,])  # Missing final index means go to the end of the array
```

Notice that there is no merge step needed, because the _Partition_ procedure ensures that, as long
as the two subarrays are sorted, then the whole array is sorted.

## Complexity

### Space

Sorts in place, so has space complexity $O(1)$.

### Time

#### Worst Case

Notice that each _Partition_ call is linear in the size of the subarray that it sorts. If the array
is already sorted, then the pivot always stays at the end of the array and you end up making $n$
calls to _Partition_. The first call costs $n$, the second costs $n-1$, ... . So the total cost is
$\sum_{i=1}^n = n(n+1)/2 ~ O(n^2)$.

#### Average Case

Won't treat this formally but will take two special cases.

##### Alternating

Imagine the splits in a recursion tree (which would be $log_2(n)$ deep if every split were even).
Since partitioning costs $O(n)$ at each level of the tree, we just need to compute the depth of the
tree. Imagine that splits (i.e. the position of the pivot) alternate between perfect (pivot in the
middle) and worst (pivot at the end), where all splits at one tree level are perfect, then they are
all worst at the next level, and so on. Then the recursion tree has depth at most $2log_2(n)$, so
the running time is still $O(nlog(n))$.

##### All Splits are 100:1 (or any constant ratio)

Similarly to the "alternating" case, we just need to consider the depth of the recursion tree. This
will be $log_{100}(n)$, so we still have a running time of $O(nlog(n))$.
