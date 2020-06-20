Algorithsm-2
------------
Undirected graph

Vertices, edge

Path. Is there a path between s and t ?
Shortest path. What is the shortest path between s and t ?
Cycle. Is there a cycle in the graph?
Euler tour. Is there a cycle that uses each edge exactly once?
Hamilton tour. Is there a cycle that uses each vertex exactly once.
Connectivity. Is there a way to connect all of the vertices?
MST. What is the best way to connect all of the vertices?
Biconnectivity. Is there a vertex whose removal disconnects the graph?
Planarity. Can you draw the graph in the plane with no crossing edges
Graph isomorphism. Do two adjacency lists represent the same graph?
Challenge. Which of these problems are easy? difficult? intractable?

Video 2-2:
Adjacency-matrix graph representation: V^2
Adjacency-list graph representation: Bag<Integer>[] adj; API

Video 2-3: Depth first search
Tremaux maze exploration

DFS (to visit a vertex v)
Mark v as visited.
Recursively visit all unmarked
vertices w adjacent to v.
public class DepthFirstPaths
{
private boolean[] marked;
private int[] edgeTo;
private int s;
public DepthFirstPaths(Graph G, int s)
{
...
dfs(G, s);
}
private void dfs(Graph G, int v)
{
marked[v] = true;
for (int w : G.adj(v))
if (!marked[w]) {
dfs(G, w);
edgeTo[w] = v;
}
}
}


Breadth-first search
Proposition. BFS computes shortest paths (fewest number of edges)
from s to all other vertices in a graph in time proportional to E + V.


Connected component: using DFS to find it

Challenges

4.2 Directed graph

Reachability
Depth-first search
exactly the same as in digraphs
	Get all vertex reachable from v
Application: find unreachable code in program; mark-sweep garbabge collector
recursively

Breadth-first search in digraphs
Same method as for undirected graphs.
・Every undirected graph is a digraph (with edges in both directions).
・BFS is a digraph algorithm.
Use Queue, shortest path

Multiple-source shortest paths
Use BFS, but initialize by enqueuing all source vertices.

Application: web crawler

topological sort
Precedence scheduling
Goal. Given a set of tasks to be completed with precedence constraints,
in which order should we schedule the tasks?

DAG. Directed acyclic graph.
Topological sort. Redraw DAG so all edges point upwards.
Reverse DFS post-order: Run depth-first search; Return vertices in reverse postorder
・If directed cycle, topological order impossible.
・If no directed cycle, DFS-based algorithm finds a topological order.

Application: java compiler does cycle detection
	A->B, B-C, C->A
Application: Excel spreadsheet recalculation

strong components
Def. Vertices v and w are strongly connected if there is both a directed path from v to w and a directed path from w to v.
Connected components vs. strongly-connected components

Application: ecological food webs
Application: software module: Subset of mutually interacting modules

Kosaraju-Sharir algorithm
Phase 1. Compute reverse postorder in GR.
Phase 2. Run DFS in G, visiting unmarked vertices in reverse postorder of GR.

Proposition. Kosaraju-Sharir algorithm computes the strong components of
a digraph in time proportional to E + V.
Implementation: easy!

Digraph-processing summary: algorithms of the day




Minimum spanning tree
Given. Undirected graph G with positive edge weights (connected).
Def. A spanning tree of G is a subgraph T that is both a tree (connected and acyclic) and spanning (includes all of the vertices).
Goal. Find a min weight spanning tree.

Def. A cut in a graph is a partition of its vertices into two (nonempty) sets.
Def. A crossing edge connects a vertex in one set with a vertex in the other.
Cut property. Given any cut, the crossing edge of min weight is in the MST.

Greedy MST algorithm
・Start with all edges colored gray.
・Find cut with no black crossing edges; color its min-weight edge black.
・Repeat until V - 1 edges are colored black.

Weighted edge API
Edge-weighted graph: array of adj[] (vetex) consists of bags of edges
Minimum spanning tree API

Kruskal's algorithm
Consider edges in ascending order of weight.
・Add next edge to tree T unless doing so would create a cycle.
Kruskal's algorithm is a special case of the greedy MST algorithm.

Challenge. Would adding edge v–w to tree T create a cycle?
Efficient solution. Use the union-find data structure.
・Maintain a set for each connected component in T.
・If v and w are in same set, then adding v–w would create a cycle.
・To add v–w to T, merge sets containing v and w.

Prim's algorithm
・Start with vertex 0 and greedily grow tree T.
・Add to T the min weight edge with exactly one endpoint in T.
・Repeat until V - 1 edges.

Pf. Prim's algorithm is a special case of the greedy MST algorithm.
・Suppose edge e = min weight edge connecting a vertex on the tree
to a vertex not on the tree.
・Cut = set of vertices connected on tree.
・No crossing edge is black.
・No crossing edge has lower weight.

Challenge. Find the min weight edge with exactly one endpoint in T.
Lazy solution. Maintain a PQ (priority queue) of edges with (at least) one endpoint in T.
・Key = edge; priority = weight of edge.
・Delete-min to determine next edge e = v–w to add to T.
・Disregard if both endpoints v and w are marked (both in T).
・Otherwise, let w be the unmarked vertex (not in T ):
– add to PQ any edge incident to w (assuming other endpoint not in T)
– add e to T and mark w

Proposition. Lazy Prim's algorithm computes the MST in time proportional
to E log E and extra space proportional to E (in the worst case).


Prim's algorithm: eager implementation
Eager solution. Maintain a PQ of vertices connected by an edge to T,
where priority of vertex v = weight of shortest edge connecting v to T.
・Delete min vertex v and add its associated edge e = v–w to T.
・Update PQ by considering all edges e = v–x incident to v
– ignore if x is already in T
– add x to PQ if not already on it
– decrease priority of x if v–x becomes shortest edge connecting x to T

Indexed priority queue: to decreaseKey(i, key)



Shortest paths in an edge-weighted digraph


Edge relaxation
Relax edge e = v→w.
・ distTo[v] is length of shortest known path from s to v.
・ distTo[w] is length of shortest known path from s to w.
・ edgeTo[w] is last edge on shortest known path from s to w.
・If e = v→w gives shorter path to w through v, update both distTo[w] and edgeTo[w].


Shortest-paths optimality conditions
Proposition. Let G be an edge-weighted digraph.
Then distTo[] are the shortest path distances from s iff:
・distTo[s] = 0.
・For each vertex v, distTo[v] is the length of some path from s to v.
・For each edge e = v→w, distTo[w] ≤ distTo[v] + e.weight().

Dijkstra's algorithm
・Consider vertices in increasing order of distance from s
(non-tree vertex with the lowest distTo[] value).
・Add vertex to tree and relax all edges pointing from that vertex.

Dijkstra’s algorithm seem familiar?
・Prim’s algorithm is essentially the same algorithm.
・Both are in a family of algorithms that compute a graph’s spanning tree.
Main distinction: Rule used to choose next vertex for the tree.
・Prim’s: Closest vertex to the tree (via an undirected edge).
・Dijkstra’s: Closest vertex to the source (via a directed path).


Acyclic edge-weighted digraphs
Proposition. Topological sort algorithm computes SPT in any edgeweighted DAG in time proportional to E + V.
edge weights can be negative!

Application: Content-aware resizing
Application: longest paths in edge-weighted DAGs (negative all weights, find shortest path)
Application: parallel job scheduling: critical path method (longest path)

Shortest paths with negative weights
Dijkstra. Doesn’t work with negative edge weights.
Re-weighting. Add a constant to every edge weight doesn’t work.

Bellman-Ford algorithm
Initialize distTo[s] = 0 and distTo[v] = ∞ for all other vertices.
Repeat V times:
- Relax each edge.

Summary

Remark 1. Directed cycles make the problem harder.
Remark 2. Negative weights make the problem harder.
Remark 3. Negative cycles makes the problem intractable.

Negative cycle application: arbitrage detection
Model as a negative cycle detection problem by taking logs.
・Let weight of edge v→w be - ln (exchange rate from currency v to w).
・Multiplication turns to addition; > 1 turns to < 0.
・Find a directed cycle whose sum of edge weights is < 0 (negative cycle).


MaxFlow
Mincut problem
Def. A st-cut (cut) is a partition of the vertices into two disjoint sets, with s in one set A and t in the other set B.
Def. Its capacity is the sum of the capacities of the edges from A to B.
Minimum st-cut (mincut) problem. Find a cut of minimum capacity.

Maxflow problem
Def. An st-flow (flow) is an assignment of values to the edges such that:
・Capacity constraint: 0 ≤ edge's flow ≤ edge's capacity.
・Local equilibrium: inflow = outflow at every vertex (except s and t).

Ford-Fulkerson algorithm
Start with 0 flow.
While there exists an augmenting path:
- find an augmenting path
- compute bottleneck capacity
- increase flow on that path by bottleneck capacity

Maxflow-mincut theorem

Relationship between flows and cuts
Def. The net flow across a cut (A, B) is the sum of the flows on its edges
from A to B minus the sum of the flows on its edges from from B to A.
Flow-value lemma. Let f be any flow and let (A, B) be any cut. Then, the net flow across (A, B) equals the value of f.

Weak duality. Let f be any flow and let (A, B) be any cut.
Then, the value of the flow ≤ the capacity of the cut.

Maxflow-mincut theorem
Augmenting path theorem. A flow f is a maxflow iff no augmenting paths.
Maxflow-mincut theorem. Value of the maxflow = capacity of mincut.


Application
Bipartite matching problem
Given a bipartite graph, find a perfect matching.

Baseball elimination problem
Q. Which teams have a chance of finishing the season with the most wins?

2012 E^2/logE (worst),  -> E
Best in practice. Push-relabel method with gap relabeling: E 3/2.

String


How to efficiently reverse a string?
StringBuilder is more efficient (rev.append(s.charAt(i)))

How to efficiently form array of suffixes?
String is more efficient (s.substring(i, N))

How long to compute length of longest common prefix?

Key-indexed counting (String sorting)
Goal. Sort an array a[] of N integers between 0 and R - 1.
・Count frequencies of each letter using key as index.
・Compute frequency cumulates which specify destinations.
・Access cumulates using key as index to move items.
・Copy back into original array.

Proposition. Key-indexed counting uses ~ 11 N + 4 R array accesses to sort
N items whose keys are integers between 0 and R - 1.
Proposition. Key-indexed counting uses extra space proportional to N + R.
Stable? Yes.

Least-significant-digit-first string sort (LSD string sort)


Most-significant-digit-first string sort (MSD string sort)

Disadvantages of MSD string sort.
・Extra space for aux[].
・Extra space for count[].
・Inner loop has a lot of instructions.
・Accesses memory "randomly" (cache inefficient).
Disadvantage of quicksort.
・Linearithmic number of string compares (not linear).
・Has to rescan many characters in keys with long prefix matches.

3-way string (radix) quicksort (Bentley and Sedgewick, 1997)
Similar to 3-way quicksort

Standard quicksort.
・Uses ~ 2 N ln N string compares on average.
・Costly for keys with long common prefixes (and this is a common case!)
3-way string (radix) quicksort.
・Uses ~ 2 N ln N character compares on average for random strings.
・Avoids re-comparing long common prefixes.

Suffix arrays
Keyword-in-context search
Suffix sort

Longest repeated substring
Suffix sort
Bad input: longest repeated substring very long.

Manber-Myers MSD algorithm overview.
・Phase 0: sort on first character using key-indexed counting sort.
・Phase i: given array of suffixes sorted on first 2i-1 characters,
create array of suffixes sorted on first 2i characters.

Worst-case running time. N lg N.
・Finishes after lg N phases.
・Can perform a phase in linear time. (!) [ahead]


Tries
R-way tries
Tries. [from retrieval, but pronounced "try"]
・Store characters in nodes (not keys).
・Each node has R children, one for each possible character.
・For now, we do not draw null links.

