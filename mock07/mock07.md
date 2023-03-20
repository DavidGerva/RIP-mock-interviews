# Mock 07 | 08/03/2023 | ale3683 vs Ranzeb

Samantha is a cartographer who is on a mission to explore a remote island in the Pacific Ocean.
Her task is to map the island's terrain and natural resources, and to do so,
she must travel from the north-east coast to the south-west coast, crossing the island through its dense forests, deserts, rivers and hills.

The island is divided into a grid of n x m cells, each of which represents a specific location on the island.
Samantha has a detailed map of the island, which shows the location of every cell.
She has not been given a specific route that she must follow to reach her destination,
and she needs to check if there exists at least one valid path from the starting point to the ending point of the island.

Your task is to create a function that takes the grid as input and determines whether there exists at least one valid path
from the starting point (0,0) to the end point (n-1,m-1) and returns it.

    O(n*m) time, O(n*m) space

    input:
    grid = [
        [0,  0,  -1,  0],
        [0,  0,   0, -1],
        [-1, -1,  0,  0],
        [0,  0,   0,  0]
    ]

    simplest case = [
      [0]
    ]

    output: (0,0)

    sample output [(0,0) , (1,1), etc..]


### Links & material
...

## Interview solution

```java
public boolean findPath(int[][] grid, boolean[][] visited, List<List<Integer>> finalPath, int x, int y) {

	if(x < 0 || x > grid.length - 1 || y < 0 || y > grid[0].length - 1) {
  	return false;
  }

	if(grid[x][y] == -1 || visited[x][y] == true) {
  	return false;
  }

  if(x == grid.length - 1 && y == grid[0].length - 1 && grid[x][y] != -1) {
  	return true;
  }

	visited[x][y] = true;


  for(int i = 0; i < 4; i++) {
		List<Integer> node = new ArrayList<>();
		node.add(x);
		node.add(y);
		finalPath.add(node);

		if()
  	if(!findPath(grid, visited, finalPath, x - 1, y)) {
    	finalPath.remove(finalPath.size() - 1);
    }

  }


  /*

  findPath(grid, visited, finalPath, x + 1, y);
  findPath(grid, visited, finalPath, x, y - 1);
  findPath(grid, visited, finalPath, x, y + 1);
	*/

	return true;
}



public List<List<Integer>> exploreIsland(int[][] grid) {
	List<List<Integer>> finalPath = new ArrayList<>();
	boolean[][] visited = new boolean[grid.length][grid[0].length];

	findPath(grid, visited, finalPath, 0, 0);

	return finalPath;
}

```
