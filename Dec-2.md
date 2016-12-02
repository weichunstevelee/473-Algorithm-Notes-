# Approximation Algorithms for TSP
Given distances between cities. Start at some point and want to go back. You want to minimize the time you spend on this tour. 
Its same as finding a Hamiltonian Cycle of minimum total edge cost. 

## Simplification?
Can assume that it is a complete graph. Can add missing edges with infinite cost to make graph complete. 

* There will always be a Hamiltonian cycle in complete graph. 

Type of TSPs:

1. Meetric-TSP: G = (V,E) is a complete graph and $c$ defines a metric space. $c(u,v)=c(v,u)$ for all $u, v$ and $c(u,w)\leq c(u, v) + c(v,w)$
for all $u,v,w$. 

2. Geometric-TSP: Special case. In Euclidean space. Distance is defined as $L_1$ norm or $L_2$ norm or something

Finding a tour in metric-complete graph is the same as allowing TSP to visit a node twice. 

## Inapproximability of TSP

1. You cannot even tell if there is a Hamiltonian path. 

If we allow that we can visit a node multiple time. 

Approximation algorithm-
__MST-Heuristic__:

  1. Compute a MST in G
  2. Obtain an Eulerian graph H = 2T by doulbing edges of T.
  3. An Eulerian tour of $H$ gives a tour of $G$ 
  4. Obtain Hamiltonian cycle by shortcutting the tour

#### Can we improve this? 
__Definition:__

An Euler tour of an undirected multigraph G=(V,E) is a closed walk that visits each edge exactly once. A graph is Eulerian if
it has an Euler tour. 

In short: Go through every edge once. 

__Observations:__

1. If all nodes have even degree, it cannot be a Tree since tree has at least one edge with odd degree. This means that there are cycles.
2. Remove a cycle every time, after removal, everyone still have even degrees, so there are still cycles.
3. Continue this, we proved that there is a Eulerian tour. 

__Observations:__ 

1. Finding optimum TSP tour in G is same as finding min cost Eulerian subgraph of G(allowing duplicate copies of edges).
2. Can we add edges (not doubling edges) to make MST Eulerian.
3. Notice that in every graph, the number of odd degree nodes is even. (This is true for all graphs).
4. Find a (min-cost) matching between odd degree nodes. 
5. Shortcutting the tour. 
6. This is $\frac{3}{2}$ approximation.

### Analysis of Chirstofides Heuristic

__Lemma__:
Cost of matching is at most $\frac{OPT}{2}$.

__Theorem__: 
Christofides heuristic returns a tour of cost at most $\frac{3OPT}{2}$

__Lemma__: 
Suppose $G=(V,E)$ is a metric and $S\subset V$ be a subset of vertices. Then there is a TSP tour in $G[S]$( the graph induced on S) of 
cost at most $OPT$. 

This is clear since if we are doing TSP in subgraph, the cost only goes down(assuming we are dealing with metric-tsp). 
And also, since we have even number of odd degrees. There is a matching of cost no more than $\frac{OPT}{2}$. There are actually two matchings and the sum of the should be $OPT$. 

Finding min-cost matching is efficient, and therefore we can use this on the Heuristic 

### Directed Graphs and Asymmetric TSP(ATSP)

Equivalent of Metric-TSP is Asymmetric-TSP(ATSP)

Allow to visit a node more than once.  

Mentioned about (min-cost) Cycle cover reduction to bipartite matching. 

We can  actually keep doing cycle cover(which is no more than OPT) until there is no edge not covered. Notice that in each iteration, you have reduce size by at least two(every cycle has at least two vertices). So we have a $log_2 n$ iterations algorithms and we can get a $log_2 n$ approximation algorithm. 

Cycle Cover $\rightarrow$ Bipartite Matching $\rightarrow$ Flow problems. 
