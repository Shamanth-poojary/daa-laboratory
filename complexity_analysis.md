# Time and Space Complexity Analysis

## 1. Merge Sort Implementation

### Time Complexity
- **Best Case:** O(n log n)
- **Average Case:** O(n log n)
- **Worst Case:** O(n log n)

**Explanation:** The array is divided into halves recursively (log n levels), and at each level, all n elements are compared and merged.

### Space Complexity
- **O(n)** - Extra space is required for the temporary array used in the merge operation.

---

## 2. Quick Sort Implementation

### Time Complexity
- **Best Case:** O(n log n) - When pivot divides array into nearly equal halves
- **Average Case:** O(n log n)
- **Worst Case:** O(n²) - When pivot is always the smallest or largest element (already sorted array)

**Explanation:** On average, partitioning divides the array into balanced halves (log n levels). In worst case, it creates unbalanced partitions leading to O(n²).

### Space Complexity
- **O(log n)** - Due to recursive call stack (average case)
- **O(n)** - In worst case due to deep recursion

---

## 3. Binary Search Tree (Insertion and Deletion)

### Time Complexity

**Insertion:**
- **Best Case:** O(log n) - Balanced BST
- **Average Case:** O(log n)
- **Worst Case:** O(n) - Skewed tree (linear chain)

**Deletion:**
- **Best Case:** O(log n) - Balanced BST
- **Average Case:** O(log n)
- **Worst Case:** O(n) - Skewed tree

**Explanation:** In a balanced BST, we traverse height (log n). In worst case, tree becomes a linked list with height n.

### Space Complexity
- **O(n)** - For storing n nodes in the tree
- **O(log n)** - Recursion stack space (average case)
- **O(n)** - Recursion stack space (worst case)

---

## 4. Breadth-First Search (BFS)

### Time Complexity
- **O(V + E)** where V = vertices, E = edges

**Explanation:** Each vertex and edge is visited exactly once. For adjacency matrix representation: O(V²).

### Space Complexity
- **O(V)** - For visited array and queue

---

## 5. Topological Sort (Using DFS)

### Time Complexity
- **O(V + E)** where V = vertices, E = edges

**Explanation:** Each vertex is visited once and each edge is examined once during DFS traversal.

### Space Complexity
- **O(V)** - For visited array, stack, and recursion call stack

---

## 6. Warshall's Algorithm (Transitive Closure)

### Time Complexity
- **O(V³)** where V = number of vertices

**Explanation:** Three nested loops iterate over all vertices. The algorithm considers each vertex as an intermediate point.

### Space Complexity
- **O(V²)** - For the adjacency matrix

---

## 7. Heap Sort Implementation

### Time Complexity
- **Best Case:** O(n log n)
- **Average Case:** O(n log n)
- **Worst Case:** O(n log n)

**Explanation:** Building heap takes O(n), and extracting each element takes O(log n). Total = n × O(log n) = O(n log n).

### Space Complexity
- **O(1)** - Sorting is done in-place, no extra space required (excluding input array)

---

## 8. Horspool's String Matching Algorithm

### Time Complexity
- **Best Case:** O(n/m) - When pattern doesn't match frequently and we skip many characters
- **Average Case:** O(n + m) where n = text length, m = pattern length
- **Worst Case:** O(n × m) - When many partial matches occur

**Explanation:** The bad-character shift allows skipping characters. However, in worst case (many false matches), we check each position multiple times.

### Space Complexity
- **O(256)** or **O(|Σ|)** - For the shift table (where Σ is the alphabet size, typically 256 for ASCII)

---

## 9. 0/1 Knapsack Problem (Dynamic Programming)

### Time Complexity
- **O(n × W)** where n = number of items, W = knapsack capacity

**Explanation:** We fill a 2D DP table of size (n+1) × (W+1), requiring O(nW) operations.

### Space Complexity
- **O(n × W)** - For the DP table
- Can be optimized to **O(W)** using 1D array, keeping only previous row

---

## 10. Prim's Minimum Spanning Tree Algorithm

### Time Complexity
- **O(V²)** with adjacency matrix (as implemented)
- **O((V + E) log V)** with binary heap and adjacency list

**Explanation:** The algorithm iterates V times. In each iteration, it searches all V vertices for minimum, then checks all V edges. Total = V × V = V².

### Space Complexity
- **O(V)** - For the sol array and other variables
- **O(V²)** - Including the input adjacency matrix

---

## 11. Kruskal's Minimum Spanning Tree Algorithm

### Time Complexity
- **O(E log E)** or **O(E log V)** where E = edges, V = vertices

**Explanation:** 
- Sorting edges: O(E log E)
- Union-Find operations: Nearly O(1) with path compression
- Total: O(E log E) for sorting dominates

**Note:** Implementation shown uses O(E²) due to finding minimum edge each time.

### Space Complexity
- **O(V)** - For parent array and edge storage
- **O(V²)** - Including input adjacency matrix

---

## 12. Dijkstra's Shortest Path Algorithm

### Time Complexity
- **O(V²)** with adjacency matrix (as implemented)
- **O((V + E) log V)** with binary heap and adjacency list

**Explanation:** V iterations, each selecting minimum distance vertex (O(V)) and updating distances for all edges (O(V)).

### Space Complexity
- **O(V)** - For distance array, parent array, visited array
- **O(V²)** - Including input adjacency matrix

---

## 13. Traveling Salesperson Problem (Exhaustive Search)

### Time Complexity
- **O(n! × n)** where n = number of nodes

**Explanation:** 
- Generate all permutations: O(n!)
- Calculate cost for each permutation: O(n)
- Total: O(n! × n)

### Space Complexity
- **O(n²)** - For weight matrix
- **O(n)** - For tour array and recursion stack

---

## 14. N-Queens Problem (Backtracking)

### Time Complexity
- **O(N!)** in worst case

**Explanation:** 
- We try placing each queen in N positions in each column
- Backtracking prunes invalid paths
- Worst case: O(N!) when exploring many invalid branches

### Space Complexity
- **O(N²)** - For the board array
- **O(N)** - For recursion stack depth

---

## 15. Subset Sum Problem (Dynamic Programming)

### Time Complexity
- **O(n × sum)** where n = number of elements, sum = target sum

**Explanation:** We fill a 2D DP table of size (n+1) × (sum+1), each cell taking O(1) to compute.

### Space Complexity
- **O(n × sum)** - For the DP table
- Can be optimized to **O(sum)** using 1D array

---

## Summary Table

| Algorithm | Time Complexity (Best) | Time Complexity (Worst) | Space Complexity |
|-----------|------------------------|-------------------------|------------------|
| Merge Sort | O(n log n) | O(n log n) | O(n) |
| Quick Sort | O(n log n) | O(n²) | O(log n) |
| BST Insert | O(log n) | O(n) | O(n) |
| BST Delete | O(log n) | O(n) | O(n) |
| BFS | O(V+E) | O(V+E) | O(V) |
| Topological Sort | O(V+E) | O(V+E) | O(V) |
| Warshall's Algorithm | O(V³) | O(V³) | O(V²) |
| Heap Sort | O(n log n) | O(n log n) | O(1) |
| Horspool | O(n/m) | O(n×m) | O(\|Σ\|) |
| 0/1 Knapsack | O(nW) | O(nW) | O(nW) |
| Prim's MST | O(V²) | O(V²) | O(V) |
| Kruskal's MST | O(E log E) | O(E log E) | O(V) |
| Dijkstra | O(V²) | O(V²) | O(V) |
| TSP | O(n! × n) | O(n! × n) | O(n) |
| N-Queens | O(N!) | O(N!) | O(N²) |
| Subset Sum | O(n × sum) | O(n × sum) | O(n × sum) |

---

## Notes

- **V** = Number of Vertices
- **E** = Number of Edges
- **n** = Number of elements/items
- **W** = Knapsack capacity (0/1 Knapsack)
- **m** = Pattern length (String Matching)
- **N** = Board size (N-Queens)
- **Σ** = Alphabet size (String Matching)
- **sum** = Target sum (Subset Sum)

