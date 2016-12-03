# Heurisitic for NP-Complete problems


## AA
Use backtracking and when you are able to solve it in efficient way, stop recursion and do that.

## Branch-and-Bound
### Goal: Solve optimization problems
Recursive Search. 
Get lower bound quickly and avoid search some paths in the tree. 
### Example: Vertex Cover

```c++
class Vertex {
public:
  bool operator>(Vertex const& v2) const {
    return _degree < v2._degree; 
  }
};
Heuristic() {
  B = 1;
  // Sort vertex by degree in set 
  // std::set<Vertex, std::greater<Vertex>> vertexSet
  for(auto v : vertexSet) {
  
  }
}
```

## Local Search 
A simple and broadly applicable heuristic method.
### Goal: Can we improve a solution?
Given a solution, is it easy to check whether I can improve something or not? 

1. First see if your solution is minimum. For example, if you remove one vertex from the solution, is it still a vertex cover.
2. If we can remove two vertices and replace it with one vertex? This is called local search.
   * Local Search: 2-change, 3-change, k-change
   * If cannot, local optimum. 
   
### Example: Traveling Salesman Problem(TSP) 
Find a Hamiltonian Cycle with minimum length.  

# Aproximation Algorithms
1. Max Knapsack
2. Min Vertex Cover
3. Min Set Cover
4. Max Independent Set
5. Min Traveling Salesman Tour

NPC problems do not look like each other in practice when it comes to approximation algorithms. Some problems are easy to solve while others are still hard. 

## Guarentee
1. Feasible solution.
2. Polynomial Time.
3. Within some percent of optimality.
### Takeaway:
1. Approximation algorithms can give us a way to distinguish the difficulty between different problems. For example, knapsack is not hard while vertex cover is hard to do very well.


### Vertex Cover:
1. Greedy Heuristic: Pick the vertex with highest degree.
  * Can be proved that: $|S| \leq (ln m + 1)\times OPT$. 
  * Can be proved that there is an infinite family of graphs where the solution S output by Greedy Heuristic is $\Omega(ln n)\times OPT$. 
  * Can be really bad as graph becomes bigger. 
4. Matchin Heuristic: 
  * Find a maximal matchin M in G
    * Keep picking edges until you cannot increase.  This is different from maximum matching.
  * S is the set of end points of edges in M. Output S.
  * Guarantee twice worse than OPT, which is very strong! 2-approximation. 
  * Can we do some local search? 
    * Yes! Make it minimum. 
    
3. LP Relaxation based approach:
  * Instead of vertex cover, LP heuristic can solve wegihted vertex cover problem. More general.
  * Minimize \sum_{v\in V} w_v x_v
  * s.t: x_u + x_v \geq 1 for each $uv \in E$
  * $x_v \in {0,1}$
  * Relax integer program to a linear program: Drop the integer constraints
  * This will give a lower bound! 

## Why approximation probolems are subtle
### Example: Independent Set
### Heuristic: Given a graph, compute a vertex cover S in G. Output V - S
Is it good? No! Not a good approximation.
Suppose k is the minimum vertex cover size. Let k = n/2 where n = |V|. Then V is a 2-approximation. But the algorithm will output an empty independent set even though there is an independent set of size n/2. 
It turns out that independent set is really really hard. But is easy to get a good approximation in vertex cover problem. This shows that problems that behave exact the same 
