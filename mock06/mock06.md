# Mock 05 | 16/11/2022 | MarcoZamboni vs HERZ

The fibonacci sequence is defined as F(1) = 1; F(2) = 1; F(N) = F(N-1) + F(N-2) for all natural numbers N except 1 and 2.
Given an index k output the k-th number of the fibonacci sequence.

    Input #1:
    k=2

    Output #1:
    1

    Input #2:
    k=7

    Output #2:
    13


### Links & material
- [Similar LeetCode problem](https://leetcode.com/problems/find-the-minimum-number-of-fibonacci-numbers-whose-sum-is-k/)

## Interview solution

```py
def fibonacci1(n):
  if n == 1 or n == 2: # b1
    return 1
  elif n in fib_res: # b2
    return fib_res[n]
  else: # b3
		fib_res[n] = fibonacci1(n - 2) + fibonacci1(n-1)
    return fib_res[n]

def fibonacci2(n):
	for i in range(3, n):


# fibonacci(5) -> 2 + 3 = 5
# fibonacci(3) -> 1 + 1 = 2
# fibonacci(4) -> 2 + 1 = 3
# tc = O(k)
# n = dimension of input
# n ~ log(k)

# O(2^n)

```

## Follow up

Assume now that your solution is called Q times in sequence with an input between 1 and K, do you want to modify your code?

```py
def test():
  for _ in range(0, Q) # i = i..Q-1
		fibonacci(randint(1, K))

# O(max(Ki))
```

Now that you’re comfortable with the Fibonacci sequence we want to decompose a natural number n
into a set of Fibonacci numbers such that their sum is equal to n,
return one set that satisfy that condition of -1 if such a set doesn’t exist


    Input #1:
    8

    Output #1:
    [8]

    Input #2:
    17

    Output #2:
    [1, 1, 2, 5, 8]