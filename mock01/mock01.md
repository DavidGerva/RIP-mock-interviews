# Mock 01 | 12/10/2022 | ranzo vs cheeto

## Exercise description

You’re given a non-empty array of positive integers where each integer represents the maximum number of steps you can take forward in the array.

For example, if the element at index 1 is 3, you can go from index 1 to index 2, 3, or 4.

Write a function that returns the minimum number of jumps needed to reach the final index.

Note that jumping from index i to index i + x always constitutes one jump, no matter how large x is.

    Sample input : array = [3, 4, 2, 1, 2, 3, 7, 1, 1, 1, 3]
    Sample output : 4 // 3 → ( 4 or 2 ) → ( 2 or 3 ) → 7 → 3.


    “””
    [1, 3, 2, 5, 3, 2]
    res = 3
    “””

## Interview solution

```py
from collections import deque

def min_number_of_jumps(arr: List[int]) -> int:
    if not arr:
        return 0
    s = set()
    res = 0
    q = deque()
    q.append(0)
    while q:
        res += 1
        size = len(q)
        for _ in range(size):
            p = q.popleft()
            s.add(p)
            for i in range(1, arr[p]+1):
                if p + i >= len(arr) -1:
                    return res
                if p+i not in s:
                    q.append(p+i)

    raise ValueError(“invalid array”)
```

[1, 3, 2, 5, 3, 2]
res = 3
s = {0, 1,2}
q = { 3, 4}

[3,10,3,2,1,...] 12
[1, 1, 1, 1, 1]

## Official solutions

Hint 1:

Try building an array of the minimum number of jumps needed to go from index 0 to all indices. Start at index 0 and progressively build up the array, using previously calculated values to find next ones.

Hint 2:

Building the array mentioned in Hint #1 should be feasible using two for loops. In an effort to optimize your algorithm, realize that at any point in the array you know the farthest index that you can reach as well as number of steps that you have left until you must “consume” a jump

Hint 3:

After initializing your maximum reach as well as your current number of steps to the value stored at index 0, you can easily update your maximum reach as you traverse the input array by simply comparing it to the value stored at each index. You can also remove one step from your current number of steps at each index, since moving from one index to the next uses up one step. When your steps reach zero, find a way to calculate how many steps you actually have left using the maximum reach and the index that you’re at.

**First solution:**


```java
public static int minNumberOfJumps(int[] array) {
    // Write your code here.
    int[] jumps = new int[array.length];
    Arrays.fill(jumps, Integer.MAX_VALUE);
    jumps[0] = 0;
    for(int i = 1; i < array.length; i++) {
      for(int j = 0; j < i; j++) {
        if(array[j] + j >= i) {
          jumps[i] = Math.min(jumps[i], jumps[j] + 1);
        }
      }
    }
    return jumps[array.length-1];
  }
```


**Optimal solution:**

```java
 public static int minNumberOfJumps(int[] array) {
    // Write your code here.
    if(array.length == 1) return 0;

    int maxReach = array[0];
    int steps = array[0];
    int jumps = 0;

    for(int i = 1; i < array.length - 1; i++) {
      maxReach = Math.max(maxReach, array[i] + i);
      steps--;

      if(steps == 0) {
        jumps++;
        steps = maxReach - i;
      }
    }

    return jumps + 1;
  }
```

## Links & material
* [Jump Game II - Greedy - Leetcode 45 - Python](https://www.youtube.com/watch?v=dJ7sWiOoK7g), Neetcode solution of similar problem