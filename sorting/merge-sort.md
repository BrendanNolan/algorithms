# Merge Sort

Assume for convenience that there are $n = 2^m$ elements, so that there are $m$ steps. Step $i$ does
$2^i$ split steps and the merging totals $n$ steps. So that's $\sum_{i=0}^m 2^i + mn$ steps i.e.
$2.2^m - 1 + mn$ steps i.e. (since $m = log(n)$) $O(nlog(n))$.
