# Depth-First Search

Let $G$ be a directed or undierected graph.

```python
def DFS(G):
    for each vertex v:
        v.colour = WHITE
        v.prev = NIL
    time = 0
    for each vertex v:
        if v.colour == WHITE
            DFS-VISIT(G, v, time)


def DFS-VISIT(G, v, time):
    ++time
    v.discovered = time
    v.color = GREY
    for each out-nbr n of v:
        if n.color == WHITE:
            n.prev = v
            DFS-VISIT(G, n, time)
    v.color = black
    ++time
    v.finished = time
```

Complexity: $O(V+E)$

**Theorem (Parenthesis Theorem):** For any two vertices, exactly one of the following is true:

- the vertices' discover-finish time intervals are disjoint and neither vertex is a descendant of
  the other in the depth-first forest
- one of the vertices' (let's say $v$'s) discover-finish time interval is contained in the other's
  (let's say $u$'s), and $v$ is a descendant of $u$ in a depth-first tree

**Theorem (White Path Theorem):** In the depth-first forest, a vertex $v$ is descended from a vertex
$u$ if and only if, at the time that $u$ is discovered, there is a path $u\rightarrow v$ consisting
entirely of white vertices.

**Corollary:** A directed graph G is acyclic if and only if a depth-first search of G yields no back
edges.

**Proof:** Clearly, if there's a back edge, then there's a cycle. Suppose that G contains a cycle
$c$. We show that a depth-first search of $G$ yields a back edge. Let $v$ be the first vertex to be
discovered in $c$, and let $(u,v)$ be the preceding edge in $c$. At time $v$ is discovered, the
vertices of $c$ form a path of white vertices from $v$ to u. By the white-path theorem, vertex $u$
becomes a descendant of $v$ in the depth-first forest, so that $(u,v)$ is a back edge.

## Edge Classifications

- **Tree Edge:** An edge in the graph which belongs to a tree in the depth-first forest
- **Forward Edge:** A non-tree edge connecting a vertex to one of its descendants in its depth-first
  tree
- **Back Edge:** An edge (obviously non-tree edge) connecting a vertex to one of its predecessors in
  its depth-first tree
- **Cross Edge:** Any other edge (can go between vertices in the same depth-first tree, as long as
  one vertex is not an ancestor of the other, or can go between vertices in different depth-first
  trees)

**Theorem: (Formulated by me, possibly suspect)** For any collection $S$ of vertices in an
_undirected_ graph, $S$ is the set of vertices of a depth-first tree if and only if it is the set of
vertices of a connected component

**Theorem:** In a DFS of an _undirected_ graph $G$, there are no cross edges.

**Proof:** This is officially a theorem. If my theorem above is correct, then it probably
immediately gives the current theorem.

## Topological Sort

**Definition:** A _topological sort_ of a _directed_ graph $G$ is a sorting of the vertices of $G$
such that every edge goes left-to-right in the vertex sorting.

We can topologically sort a DSG just by running DFS and sorting vertices in descending order of
finishing time. The easiest way to do that is just to run DFS and, whenever a vertex is finished,
insert it at the beginning of a list.

## Strongly Connected Components
