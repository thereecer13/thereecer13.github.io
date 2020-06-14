---
layout: post
title:  "Project Euler Problem #1"
date:   2020-06-12 16:46:09 -0700
categories: jekyll update
---
For this blog post I want to explore the first [Project Euler][project-euler] problem:
> If we list all the natural numbers below 10 that are multiples of 3 or 5, we get 3, 5, 6 and 9. The sum of these multiples is 23.
>
> Find the sum of all the multiples of 3 or 5 below 1000.

One way to solve this is to iterate through all numbers from 3 to 1000, figure out which numbers are divisible by 3 or 5, and sum up those numbers. This can be written in Python3 as:

```python
tot = 0
for i in range(3, 1000):
	if i % 3 == 0 or i % 5 == 0:
		tot += i
print(tot)
```
```python
233168
```

There is another solution. The sum of all integers from 1 to n can be calculated using the formula:

$$ 1 + 2 + 3 + \cdots + n = \frac{n(n+1)} {2} $$

We can see that the above is equivalent to calculating the sum of all multiples of 1 up to n. Expanding this to the multiples of 3 gives: 

$$ 3 + 6 + 9 + \cdots + 3n = 3 \times (1 + 2 + 3 + \cdots + n) = 3 \times \frac{n(n+1)} {2} $$

If $3n$ represents a multiple of 3, then the value of $n$ should be the largest integer that satisfies $3n < 1000$, which means that $n$ should be 333. We can do the same for 5 and find that the value for $n$ should be 199. One thing we need to do is make sure that we aren't double counting. Since 3 and 5 both go into 15, this means that we must subtract all multiples of 15 that are less than 1000. Thus we can calculate the answer by doing the following calculation: 

$$ 3 \times \frac{333(333+1)} {2} + 5 \times \frac{199(199+1)} {2} - 15 \times \frac{66(66+1)} {2} $$

```python
threes = 3 * (333 * (333 + 1) // 2)
fives = 5 * (199 * (199 + 1) // 2)
fifteens = 15 * (66 * (66 + 1) // 2)
print(threes + fives - fifteens)
```
```python
233168
```


[project-euler]: https://projecteuler.net/
