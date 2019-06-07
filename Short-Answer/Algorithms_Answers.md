Add your answers to the Algorithms exercises here.

# Analysis of Algorithms

## Exercise I

Give an analysis of the running time of each snippet of pseudocode with respect to the input size n of each of the following:

```
a)    a = 0
      while (a < n * n * n):
          a = a + n * n
```

Despite the gaggle of ns here, this code snippet is O(n) time complexity - that is, the while loop will run n times. One way to think about it is that the `n * n` in the while condition and `n * n` inside the loop can each be replaced with a 1, yielding:

```
      a = 0
      while (a < n * 1):
          a = a + 1
```

and then:

```
      a = 0
      while (a < n):
          a = a += 1
```

During each loop, a will take one step toward n.
