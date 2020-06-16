---
layout: post
mathjax: true
title:  "Project Euler Problem #1"
date:   2020-06-12 16:46:09 -0700
categories: jekyll update
---
For this blog post I want to explore the first [Project Euler][project-euler] problem:
> If we list all the natural numbers below 10 that are multiples of 3 or 5, we get 3, 5, 6 and 9. The sum of these multiples is 23.
>
> Find the sum of all the multiples of 3 or 5 below 1000.

We can solve this simply by iterating through all numbers from 3 to 1000, figuring out which numbers are divisible by 3 or 5, and summing up those numbers. This can be written as a one liner in Python 3:

```python
print(sum([i for i in range(3, 1000) if i % 3 == 0 or i % 5 == 0]))
```
```python
233168
```

Let's expand this problem a little further. What if instead of finding the sum of multiples below 1000, we find the sum of multiples below any natural number $N$? The time complexity of the above is O(n), so it can get quite slow at large $N$. However, there is another approach. The sum of all integers from 1 to n can be calculated using the formula:

$$ 1 + 2 + 3 + \cdots + n = \frac{n(n+1)} {2} $$

We can see that the above is equivalent to calculating the sum of all multiples of 1 up to n. Expanding this to the multiples of 3 gives: 

$$ 3 + 6 + 9 + \cdots + 3n = 3 \times (1 + 2 + 3 + \cdots + n) = 3 \times \frac{n(n+1)} {2} $$

Going back to the Project Euler question, if $3n$ represents a multiple of 3, then the value of $n$ should be the largest integer that satisfies $3n < N$. If we do the same with 5, then the answer can be obtained by adding together the individual sum of multiples (below 1000) for both 3 and 5. But wait! Doing this would double count all shared multiples between 3 and 5. To fix this, we subtract all multiples of the lowest common multiple of 3 and 5, i.e. 15, below $N$ from the sum of the multiples of 3 and 5 below $N$. 

```python
N = 1000  # Can be any positive integer
def sumOfMult(base, max_n):
	max_mult = (max_n - 1) // base
	return(base * (max_mult * (max_mult + 1)) // 2)
print(sumOfMult(3, N) + sumOfMult(5, N) - sumOfMult(15, N))
```
```python
233168
```

Now we can change the value of `N` to whatever positive integer value we want. Note that the above runs in constant time because changing the value of `N` only changes the values in the equation discussed above.

What if we expanded this question even further by trying to find the sum of the multiples of any number of integers such that the multiples are below `N`? We must now think of what happens when we consider other numbers besides 3 and 5. We employ the same idea as before, where we sum the multiples of all input integers, and subtract the multiples of their lowest common multiples. Here I create a separate function, `findCommonMults`, that finds all the lowest common multiples between the input integers.

```python
arr = [3, 5] # Input array of integers
N = 1000

def sumOfMult(base, max_n):
    max_mult = (max_n - 1) // base
    return(base * (max_mult * (max_mult + 1)) // 2)

# Find common multiples
def findCommonMults(array):
    mult_arr = []
    for i in range(len(array) - 1):
        for j in range(i + 1, len(array)):
            mult_arr.append(array[i] * array[j])
    return mult_arr
mult_arr = findCommonMults(arr)

ans = sum([sumOfMult(i, N) for i in arr]) - sum([sumOfMult(j, N) for j in mult_arr])
print(ans)
```
```python
233168
```

Now we can feed our script any number of input integers in an array as well as the maximum number `N` that the multiples must be below. That's all for now!	

*** 

##### Please send comments, questions, or concerns to my email. The code for everything in this post can be found on my [GitHub][github] page.

[project-euler]: https://projecteuler.net/
[github]: https://github.com/thereecer13
