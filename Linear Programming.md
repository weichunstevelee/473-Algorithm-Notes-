# Linear Programming

## Example
Maximum Flow in Network

For a general flow network G=(V,E) with capacities c_e on edge e in E, we have variables f_e indicating flow on edge e

1. Maximize: \sum_{e\in E} f_e
2. Constraints:
  a. f_e \leq c_e  
  b. \sum_{e out of v} f_e - \sum_{e into v} f_e = 0
  c. f_e \geq 0

m variables, m+n-2+m constraints

## Canoncial Form
A lienar program is in canonical form if it has the following structure:

1. Maximize: \sum_{j=1}^d 
2. Constarints:
  a. \suM_{j=1}^d a_{ij} x_j \leq b_i for i = 1...n
  

## Feasible Region and Convexity 
1. A constraint holds with equlaity, we say the constraint/hyperplane i is tight. 
2. Notice that an interior point in a convex set can be represented as x = a1x1 + 2ax2 + ... + anxn, where a_i>=0 and \sum_{i} a_i = 1. Then we must have min_i a_i \leq a \leq max_i a_i. This implies that the optimal value is located on the boundary.

## How to solve?
Simplex 
Move from a vertex to its neighboring vertex. 

1. Which vertex should I go? 
2. When to stop? How do I know I reach maximum?

### Observations 
Suppose we are at a non-optmila vertex x and optmial is x^*, then cx^* > cx. 
How does (cx) change as we move from x to x^* on the line joining the two?

1. Strictly increases! Because d = x^*-x is the direction from x to x^*.
2. cd = cx^* - cx > 0.
3. In x' = x + \delta*d as \delta goes from 0 to 1, we move from x to x^*.
4. cx' = cx + \delta(cd). Strictly increasing with \delta! 
5. Due to convexity, all of these are feasible points. 

Conclusion: There exists a direction such that we can improve the value. 
Question: How to do that? 

## Cone
Definition:
Given a set of vectors D = {d_1, d_2, ..., d_k}, the cone spanned by them is just their positive linear combinations, i.e.,
cone(D) = {d|d=\sum_{i=1}^k \lambda_i d_i, where \lambda_i \geq 0, \forall i} 

### Cone at Vertex 
Let z_1, ..., z_k be the neighboring vertices of x. And let d_i = z_i - x be the direction from x to z_i. 
__Lemma__ 
Any feasible direction of movement d from x is in the cone({d_1, d_2, ..., d_k}). 

Conclusion: Any feasible movement from a vertex __is in the cone at the vertex__. 
__Lemma__
If d\in cone({d_1, ..., d_k}) and (cd) > 0, then there is exists d_i such taht (cd_i) > 0. 

__Proof__
The the contrary, assume (c d_i) \leq 0 for all i. Since d is a positive linear combination of d_i, (cd) = (c \sum_{i=1}^k \lambda_i d_i) = \sum_{i=1}^k \lambda_i(c\dot d_i) \leq 0. A contradiction. 
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
Fix a vertex x. Let the 
