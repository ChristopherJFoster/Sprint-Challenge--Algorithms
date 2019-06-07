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

## Exercise II

Suppose that you have an _n_-story building and plenty of eggs. Suppose also that an egg gets broken if it is thrown off floor _f_ or higher, and doesn't get broken if dropped off a floor less than floor _f_. Devise a strategy to determine the value of _f_ such that the number of dropped eggs is minimized.

Write out your proposed algorithm in plain English or pseudocode and give the runtime complexity of your solution.

#### Answer (to minimize broken eggs):

##### Strategy:

I would drop an egg off floor 1 and note if it breaks. If the egg breaks, then _f_ = 1. If the egg doesn't break, I would move up to floor 2 and drop another egg. If the egg breaks, then _f_ = 2. Assuming _f_ <= _n_ and _n_ < infinity, I would keep moving up one floor at a time until an egg breaks and thus the value of _f_ is determined. This solution should only require a single egg to be broken. The runtime complexity is **O(_n_) time complexity** (since I might have to go all the way to the top floor (floor _n_) to determine the value of _f_) and **O(1) space complexity** (since there is no significant increase in memory needed for even a large _n_).

##### Pseudocode:

```
      def eggdropper(n):
          for f in range(1, n + 1):
              drop egg from floor f
              if egg breaks:
                  return f
```

## New answer, now that I understand that the question is asking to minimize the number of dropped eggs:

#### Answer (to minimize dropped eggs):

##### Strategy:

I would drop an egg off the floor that is halfway up the full height of the building. If the egg breaks, I would move down to the floor that is halfway between the floor I was just on and the bottom floor. If the egg doesn't break, I would move up to the floor halfway between the floor I was on and the top floor. Either way, I would drop another egg and move down if it breaks, and up if it doesn't. Each drop eliminates about half of the remaining available floors. Eventually I would find the floor where an egg does not break if dropped, but if dropped from the floor above, the egg does break: this is floor _f_.

My strategy is a binary search. Assuming _f_ <= _n_ and _n_ < infinity, the runtime complexity is **O(log(_n_)) time complexity** (since I eliminate half the floors with each drop) and

**O(1) space complexity** (since there is no significant increase in memory needed for even a large _n_).

##### Pseudocode:

```
      def eggdropper(building, low=1, high=None):
          if high == None:
              high = height(building)
          while low < high:
              mid = low + (high - low) // 2
              drop egg from floor mid:
                  if egg breaks:
                      high = mid
                  else:
                      low = mid
          return low

```
