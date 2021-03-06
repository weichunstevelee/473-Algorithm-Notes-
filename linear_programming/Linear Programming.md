<script type="text/javascript" src="http://cdn.mathjax.org/mathjax/latest/MathJax.js?config=default"></script>

# Linear Programming

## Example
Maximum Flow in Network

For a general flow network G=(V,E) with capacities c_e on edge e in E, we have variables f_e indicating flow on edge e

1. Maximize: $\sum_{e\in E} f_e$
2. Constraints:

  a. $f_e \leq c_e$  
  b. $\sum_{e out of v} f_e - \sum_{e into v} f_e = 0$
  c. $f_e \geq 0$

m variables, m+n-2+m constraints

## Canoncial Form
A lienar program is in canonical form if it has the following structure:

1. Maximize: \sum_{j=1}^d 
2. Constarints:

  a. \sum_{j=1}^d a_{ij} x_j \leq b_i for i = 1...n
  

## Feasible Region and Convexity 
1. A constraint holds with equlaity, we say the constraint/hyperplane i is tight. 
2. Notice that an interior point in a convex set can be represented as $x = \sum_{i}a_ix_i $, where $a_i\geq0$ and $\sum_{i} a_i = 1$. Then we must have $min_i a_i \leq a \leq max_i a_i$. This implies that the optimal value is located on the boundary.

## How to solve?
Simplex 
Move from a vertex to its neighboring vertex. 

1. Which vertex should I go? 
2. When to stop? How do I know I reach maximum?

### Observations 
Suppose we are at a non-optmila vertex x and optmial is $x^{opt}$, then $c\dot x^{opt} > c\dot x$. 
How does $(c\dot x)$ change as we move from $x$ to $x^{opt}$ on the line joining the two?

1. Strictly increases! Because $d = x^{opt}-x$ is the direction from $x$ to $x^{opt}$.
2. $c\dot d = c\dot x^{opt} - c\dot x > 0$.
3. In $x' = x + \delta d$ as $\delta$ goes from 0 to 1, we move from $x$ to $x^{opt}$.
4. $c\dot x' = c\dot x + \delta(c\dot d)$. Strictly increasing with $\delta$! 
5. Due to convexity, all of these are feasible points. 

Conclusion: There exists a direction such that we can improve the value. 
Question: How to do that? 

## Cone
Definition:
Given a set of vectors $D = \{d_1, d_2, ..., d_k\}$, the cone spanned by them is just their positive linear combinations, i.e.,
$cone(D) = \{d|d=\sum_{i=1}^k \lambda_i d_i, where \lambda_i \geq 0, \forall i\} $

### Cone at Vertex 
Let $z_1, ..., z_k$ be the neighboring vertices of x. And let $d_i = z_i - x$ be the direction from x to $z_i$. 
__Lemma__ 
Any feasible direction of movement d from x is in the $cone(\{d_1, d_2, ..., d_k\})$. 

Conclusion: Any feasible movement from a vertex __is in the cone at the vertex__. 
__Lemma__
If $d\in cone({d_1, ..., d_k})$ and $(c\dot d) > 0$, then there is exists $d_i$ such taht $(c\dot d_i) > 0$. 

__Proof__
The the contrary, assume $(c\dot d_i) \leq 0$ for all i. Since d is a positive linear combination of $d_i$, $(c\dot d) = (c \sum_{i=1}^k \lambda_i d_i) = \sum_{i=1}^k \lambda_i(c\dot d_i) \leq 0$. A contradiction. 
Conclusion: 

Conclusion : 

1. If there is a direction of improvement, then there is at least a neighbor where the cost/value improves.
2. How many neighbors are there we can improve? 

  a. 0-dimensional face: Vertex, 1D face: Edge, (d-1)D face: Hyperplane.
  
  b. r linearly independent tight hyperpalnes forms d-r dimensional face. (2 independent tight lines you get a edge). 
  
  c. Vertices being of 0D, d linear independent tight hyperplanes. 


Observation:

1. Which neighbor to move to? One where objective value increases.
2. When to stop? When no neighbor with better objective value. Notice that if there higher objective value, based on lemmas, there must be a neighbor of higher objective value(cone lemma).
3. How much time doest it take? At most d neighbors to consider in each step.

Simplex Algorithm:

1. Start at a vertex of the polytope.
2. Compare value of objective function at each of the d neighbors.
3. Move to neighbor that improves objective function, and repeat step 2.
4. If no improving neighbor, then stop. 

Super fast! Smooth analysis can prove that. Check it out. 

## Implementation
### Moving to a Neighbor
Fix a vertex x. Let the d hyperplanes/constraints tight at x be,

$$ \sum_{j=1}^d a_{ij}x_j = b_i,~1\leq i\leq d$$
(Can also be written in matrix form) 

A neighbor vertex $x'$ is connected to $x$ by an edge. D-1 hyperplanes tight on this edge. To reach x', one hyperplane has to be relaxed, while maintaining other d-1 tight constraints.

#### How far should we move?
Move in $d_i$ direction from $x$ to $x+\epsilon d_i$ and stop when we hit a new hyperplane. 
__Need ot ensure feasibility__. 
Let $A_k$ be the $k^{th}$ row of A


## Computing Starting Vertex
This is equivalent to solve another LP!
New LP:
Find an x such that $Ax\leq b$
If $b\geq 0$ then trivial, $x=0$, otherwise:
$min:s$
$s.t.: \sum_j a_{ij}x_{j} - s \leq b_i,~\forall i$
$s\geq 0$. 

Don't fall into recursion! And try to solve another LP. 
Trivial feasible solution: 
$x = 0, s = |min_i b_i|$
If $Ax\leq b$ feasible, then optimal value of the above LP is $s=0$. 


To important aspects:
1. How to know it is infeasible: It sounds like we can solve the LP for starting point and find that objective value is positive if the original LP is infeasible. 
2. Unbounded: NextVertex algorithm will return NULL.


## Degeneracy and Cycling
More than d constraints are tight at vertex x. Say d+1. Suppose we pick first d to form A, and compute directions $d_1, d_2, ..., d_d$. Then NextVertex(x, d_i) will encounter $(d+1)^{th}$ constraint with $\epislon = 0$ as an upper bound. Hence we never move. This can be avoided by adding small random perturbation to $b_i$s. 

## Feasible Solutions and Lower Bounds
Consider the program 

1. Maximize $4x_1 + 2x_2$.
2. Subject to:
  
  a. $x_1 + 3x_2\leq 5$
  b. $2x_1 - 4x_2 \leq 10$
  c. $x_1 + x_2 \leq 7$
  d. $x_1 \leq 5$
