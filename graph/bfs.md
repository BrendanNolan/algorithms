# Breadth-First Search

# The Algorithm

We use vertex colours to indicate discovery state:

- White for undiscovered
- Grey for discovered but not finished
- Black for finished

```python
def bfs(graph, source):
    for v in graph - {source}:
        vertex.colour = white
        vertex.dist = infty
        vertex.prev = None
    source.colour = grey
    source.dist = 0
    source.prev = NIL

    queue = [source]
    while not queue.empty():
        v = queue.pop()
        for nbr in v.neighbours():
            if nbr.colour == white:
                nbr.colour = grey
                nbr.dist = v.dist + 1
                nbr.prev = v
                queue.push(nbr)
        v.colour = black
```

## Complexity

No vertex is ever whitened, so each vertex is enqueued at most once and hence dequed at most once.
Since a vertex's incident edges are scanned only when the vertex is dequeued, each edge is traversed
at most once, so the complexity if $O(E + V)$.

## Proof The Algorithm Works

Let $\delta(s, v)$ be the shortest distance from a vertex `s` to a vertex `v`.

`Lemma:` Let `G` be a directed or undirected graph and `s` be any vertex of `G`. Then for any edge
`(u, v)` in `G`, we have $\delta(s, v) \leq \delta(s, u) + 1$. `Proof:` Totally obvious.

`Lemma:` At any point during `BFS`, the queue contains vertices whose `.distance` vales are
non-strictly increasing from the queue's head to it's tail; morevoer the tail vertex's `.distance`
value is at most one larger than the head vertex's. `Proof:` Not that easy to prove formally but
think of it like this: if it were not the case, then it would violate the breadth-first nature of
breadth-first search.

`Corollary:` Suppose that vertices `a` and `b` are enqueued during `BFS` and that `a` is enqueued
before `b`. Then, when `b` is enqueued, we have `a.distance <= b.distance`. `Proof:` Immediate from
the previous lemma.

`Theorem:` `BFS` finds all reachable vertices and assigns them `.distance` values which are equal to
their shortest-path distances from the source vertex.
