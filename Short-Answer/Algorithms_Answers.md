Add your answers to the Algorithms exercises here.

# Analysis of Algorithms

## Exercise I

Give an analysis of the running time of each snippet of pseudocode with respect to the input size n of each of the following:

#### Question a:

```
a)    a = 0
      while (a < n * n * n):
          a = a + n * n
```

#### Answer a:

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

#### Question b:

```
b)    sum = 0
      for i in range(n):
          i += 1
          for j in range(i + 1, n):
              j += 1
              for k in range(j + 1, n):
                  k += 1
                  for l in range(k + 1, 10 + k):
                      l += 1
                      sum += 1
```

#### Answer b:

Nested for loops quickly rack up time complexity. This code snippet can be considered O(n^4) time complexity. The fact that the ranges don't start at zero drops the number of operations slightly, but the drop becomes insignificant as n gets larger. As written, this code would chug at even a modest n on most machines.

#### Question c:

```
c)    def bunnyEars(bunnies):
          if bunnies == 0:
          return 0

      return 2 + bunnyEars(bunnies-1)
```

#### Answer c:

The time complexity of this code snippet is O(n) (or O(bunnies), haha). Notably, however, since the function is recursive—calling an additional function for each additional n—its space complexity is also O(n). This function is thus not especially performant as it will reach maximum recursion depth fairly quickly. A much more performant (and simpler) solution:

```
      def simplerBunnyEars(bunnies):
          return 2*bunnies
```
