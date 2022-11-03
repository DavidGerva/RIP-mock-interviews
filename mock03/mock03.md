# Mock 03 | 02/11/2022 | ale3683 vs Marco Zamboni

## Exercise description

You have a graph of n nodes.
You are given an integer n and an array edges where edges[i] = [ai, bi] indicates that there is an edge between ai and bi in the graph.
Return true if there's more than one component otherwise false.
There are no repeated edges.

    input #1:
    n = 5, edges = [[0,1],[1,2],[3,4]]

    output #1:
    true

    why?
    there are two components: 0-1-2         3-4

    input #2:
    n = 5, edges = [[0,1],[1,2],[2,3],[3,4]]


    output #2:
    false

    why?
    there is just one component: 0-1-2-3-4

## Follow Up
- follow-up 1: If you can change the input to have already the adjs list built what that would change in time complexity?
- follow-up 2: How you would count how many components we have in the graph?
- follow-up 3: How you would count how many edges we need to add to have just one component?
- follow-up 4: How you would findout between which nodes we need to add an edge to have just one component?

DFS:

    TC: O(E+V)
    SC: O(E+V) //no accounting for adj list, but for the stack

BFS:

    TC: O(V+E)
    SC: O(V) //no accounting for adj list

union find path compression || rank:

    TC: O(V+logE) //no accounting for adj or directly calling on the edges, list otherwise O(E+V)
    SC: O(V) //no accounting for adj list

union find path compression + rank:

    TC: O(E⋅α(n)) //no need of an adj list, otherwise O(E+V), with parent optimization on the fly
    SC: O(V) //no accounting for adj list

### Links & material
The proposed problem il similar to LeetCode [323: Number of Connected Components in an Undirected Graph](https://leetcode.com/problems/number-of-connected-components-in-an-undirected-graph/description/). (for premium users)

* [323 - Number of Connected Components in an Undirected Graph on leetcode.ca](https://leetcode.ca/2016-10-18-323-Number-of-Connected-Components-in-an-Undirected-Graph/)
* [323 - Number of Connected Components in an Undirected Graph NeetCode youtube solution](https://www.youtube.com/watch?v=pXNIwu3uDnA)


## Interview solution

```py
def dfs(graph: list[list[int]], node: int, visited: set):
	visited.add(node)
  for connected in graph[node]:
  	if connected not in visited:
    	dfs(graph, connected, visited)

def determine_connectiveness(n: int, edges: list[list[int, int]]) -> bool:
	graph = [list() for _ in range(n)]
  for from, to in edges:
  	graph[from].append(to)
    graph[to].append(from)

  visited = set()
  dfs(graph, 0, visited)
  return len(visited) != n

n = 5, edges = [[0,1],[1,2],[3,4]]

```

    graph = [[1], [0, 2], [1], [4], [3]]
    visited = {0, 1, 2}
    return True

O(N + M) M: size(edges), N

## Follow Up

```py
def dfs(graph: list[list[int]], node: int, visited: set):
	visited.add(node)
  for connected in graph[node]:
  	if connected not in visited:
    	dfs(graph, connected, visited)

def determine_connectiveness(n: int, edges: list[list[int, int]]) -> bool:
	graph = [list() for _ in range(n)]
  for from, to in edges:
  	graph[from].append(to)
    graph[to].append(from)

  visited = set()
  num_components = 0
  new_edges = []
  for node range(n):
  	if node not in visited:
    	num_components += 1
  		dfs(graph, node, visited)
      if node != 0:
      	new_edges.append([node, 0])
  assert len(new_edges) == num_components - 1
  return new_edges

```

O(NM)
O(M)

Union find use:

```py
class UFDS:
	def __init__(n: int):
  	self.parents = [None for _ in range(n)]

  def find(x):
  	if self.parent[x] is not None
  		p = find(self.parent[x])
      self.parent[x] = p
    	return p
    return x

  def same_set(x, y):
  	return find(x) == find(y)

  def union(x, y):
  	x, y = find(x), find(y)
    self.parent[x] = y




def determine_connectiveness(n: int, edges: list[list[int, int]]) -> bool:
  ufds = UFDS(n) # O(N)
  for from, to in edges:
    ufds.union(from, to) # amort. O(1)
  return not all(something(map(ufds.find, range(n)))) # O(N)

```

Time O(N + M)
Memory O(N)
