# Minimum Spanning Trees (MSTs)

**Definition:** A _minimum spanning tree_ for a connected acyclic graph $G$ is a subtree where the
sum of the edge weights is as small as possible.

Not that to specify a subtree of a graph, it is enough to specify the edges.

## Generic Method

The generic method grows the MST one edge at a time, maintaining at each iteration a set of edges
$A$ which is a subset of some MST.

At each step, we determine an edge $e$ that we can add to $A$ without violating the invariant that
$A$ is a subset of some MST. We call such an edge a _safe edge_ for A.

```python
def Generic_Build_MST(graph):
    A = {}
    while A is not an MST:
        find an edge e that is safe for A
        add e to A
    return A
```

## Algorithm For Finding A Safe Edge

**Definition:** A _cut_ of a graph is just a partition of its vertices into two portions.

**Definition:** An edge of a graph _crosses_ a cut if the edge's source and target are in different
portions of the cut.

**Definition:** A cut of a graph $respects$ a set $A$ of edges if no edge of $A$ crosses the cut.

**Definition:** A _light edge_ satisfying a property $P$ is an edge which is as light as possible
among all edges satisfying $P$.

**Theorem:**

- Let $A$ be a subset of edges that is included in some minimum spanning tree for $G$
- Let $C$ be any cut of G that respects $A$

Then any light edge crossing $C$ is safe for $A$.

**Proof:**

Let $T$ be a MST that includes $A$ and let $(u,v)$ be a light edge crossing $A$. Aassume that $T$
does not contain $(u,v)$ (since we are done if it does). We will construct another MST $T'$ which
includes $(u,v)$.

Consider the simple path $p$ in $T$ from $u$ to $v$; we get a cycle by adding $(u,v)$ to this path.
Notice that, since $u$ and $v$ are on opposite sides of the cut $C$, at least one edge $(x,y)$ in
$p$ also crosses $C$.

_Note:_ $(x,y)$ is not in $A$ since $A$ respects $C$.

Removing $(x,y)$ from $T$ will break $T$ into two components; adding $(u,v)$ back in will form a new
spanning tree $T'$.

$T'$ is clearly minimum since $(u,v)$ is light.

Since $A\subseteq T$, we also have $A \cup (u,v) \subseteq T \cup (u,v)$. Since, as noted above,
$(x,y) \notin A$, we have $A\cup (u,v) - (x,y) \subseteq T \cup (u,v) - (x,y) = T'$, so that $(u,v)$
is safe for $A$.
