# Linear Programming

## Example
Maximum Flow in Network

For a general flow network G=(V,E) with capacities c_e on edge e in E, we have variables f_e indicating flow on edge e
Maximize: \sum_{e\in E} f_e
Constraints:
1. f_e \leq c_e  
2. \sum_{e out of v} f_e - \sum_{e into v} f_e = 0
3. f_e \geq 0

m variables, m+n-2+m constraints
