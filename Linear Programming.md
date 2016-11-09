# Linear Programming

## Example
Maximum Flow in Network

For a general flow network G=(V,E) with capacities c_e on edge e in E, we have variables f_e indicating flow on edge e
1Maximize: \sum_{e\in E} f_e
Constraints:

1. f_e \leq c_e  
2. \sum_{e out of v} f_e - \sum_{e into v} f_e = 0
3. f_e \geq 0

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
