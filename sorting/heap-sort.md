# Heap Sort

## Heaps

**Definition:** A _complete binary tree_ is a binary tree which is completely filled on all levels
except possibly the lowest, which is filled from the left up to a point.

Suppose we list the nodes of a complete binary tree in an array $A$ in the obvious way (with indices
starting at zero for both the array and the tree levels). Let $x$ be the $nth$ element at level $m$.
Then $x$ has $2^0 + ... + 2^{m-1} = 2^m - 1$ elements above it and n elements to its left, so $x$ is
at position $2^m + n - 1$ in the array. Now, using this formula to express the positions of $x$'s
parents and children, we get the following formulae for the positions of the parents and children of
the $ith$ element of the array:

- `parent(i) == floor(i/2)`
- `left_child(i) = 2i`
- `right_child(i) = 2i + 1`

## Max Heaps (Min Heaps Are Obviously Similar)

**Definition:** A _max heap_ is a complete binary tree where the key of any node is greater than
that of its children.

## Operations On Max Heaps

### Max_Heapify

Suppose that $A$ is a complete binary tree and the left and right subtrees of the root are max
heaps. We can turn $A$ into a max heap by applying the _Max_Heapify_ procedure.

**Definition:** _Max_Heapify_ allows the root key to "float down" the tree by swapping the key with
the key of its smaller child until the key ios greater than that of both its children.

Clearly, _Max_Heapify_ turns the tree back into a heap and runs in $O(log(n))$ time.

### Build_Max_Heap

Suppose that A is a complete binary tree (i.e. just an array) and we want to turn it into a max
heap.

**Definition:** _Build_Max_Heap_ starts at the right-hand side of the second-last row of the tree
and walks backwards through the array, calling _Max_Heapify_ on each node.

Clearly, _Build_Max_Heap_ builds a max heap and runs in $O(nlog(n))$ or better. In fact, since most
nodes are near the bottom of the tree, they don't have far to go to float down, so that
_Build_Max_Heap_ runs in $O(n)$ time.

### Heap Sort

To sort an array $A = a_0, \ldots , a_n$:

- Run _Build_Max_Heap_
- Move the tree root element to the end of the array. Consider the root as being removed from the
  heap, so that $a_0, \ldots, a_{n-1}$ represent the heap.
- Move $a_{n-1}$ to the root position in the heap and call _Max_Heapify_
- Continue doing this until the heap is emptied

This means one call to _Build_Max_Heap_ and $n$ calls to _Max_Heapify_, which means $O(n + nlog(n))$
i.e. $O(nlog(n))$.

# Priority Queues

A max priority queue $Q$ should support the following operations: _Max_, _Extract_Max_,
_Increase_Key_, _Insert_, _Decrease_Key_. We will leave _Decrease_Key_ for later.

If we implement the queue as a max heap, then we can implement the priority-queue operations as
follows:

## Max ( O(1) )

Easy - just return the key of the root. $O(1)$.

## Extract_Max ( O(logn) )

- Set $m$ equal to the key at the root
- Swap the keys of the root and the last node
- Run _Max_Heapify_ on the new root node
- Return $m$

## Increase_Key ( O(logn) )

- Set the new key of the node
- While the node key is larger than its parent's key, swap the node and its parent

## Insert ( O(logn) )

- Insert the desired node at the end of the heap with key $-\infty$ (so that the heap property is
  clearly preserved)
- Run _Increase_Key_ to set the node to its desired key
