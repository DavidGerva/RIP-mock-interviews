# Mock 06 | 02/03/2023 | MarcoZamboni vs you_33

You are a visitor in the capital city of Algoland and you need to attend an algorithm conference tomorrow morning.
Tonight instead you'll attend a party and probably go to bed quite late, but since you really value your sleep you want to find what is the latest time you can depart from your hotel when going the the conference.
We can see the city as a system of streets and interceptions, each street connects 2 interceptions, can be walked in both directions and take some time to be walked.
Intersections are numbered from 0 to N-1, your hotel is located at intersection 0 and the conference venue at intersection N-1.
What is the latest time t you can depart from your hotel if you want to arrive at the conference at time t_0 = 0? (Note that t will be a negative number)

The input contains the number N of intersection and a list of streets, each street is defined by three numbers: a, b and t, it connects intersections a and b and takes t time to be walked.


### Example
In:

    5
    0 1 6
    0 3 1
    1 2 2
    1 3 2
    1 4 5
    2 3 1
    2 4 5

Out:

    7

Path:

    0 -> 3 -> 2 -> 4


## Interview solution

```py
#intersection = node
#street = edge
#
graph = {
  0 : [(1,6), (3,1)]
}


def Solution(N: int, streets: list[tuple[int, int, int]]):
  graph = defaultdict(list)
  for street in streets: # O(E)
    graph[street[0]].append((street[1],street[2]))
    graph[street[1]].append((street[0],street[2]))
  MAX_FLOAT = float("inf")
  distances = {node:MAX_FLOAT for node in range(0,n-1)} # O(V)
  distances[start]=0
  queue = heap([(0,0)])

  while queue:
    (distance, node) = queue.pop() #O(1)
    if distance > distance[node]:
        continue
    for neighbor in graph[node]:
      d = neighbor[1] + distance #(1)
      if d < distances[neighbor[0]]: #(1)
      	distances[neighbor[0]] = neighbor[1] + distance #(1)
        queue.update((d, neighbor)) #(LOG(V)))
  #(V+E*Log(E))
  return 0-distance[N-1]


```