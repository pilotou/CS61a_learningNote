# Required Questions

### Q1: GCD

The greatest common divisor of two positive integers `a` and `b` is the largest integer which evenly divides both numbers (with no remainder). Euclid, a Greek mathematician in 300 B.C., realized that the greatest common divisor of `a` and `b` is one of the following:

- the smaller value if it evenly divides the larger value, or
- the greatest common divisor of the smaller value and the remainder of the larger value divided by the smaller value

In other words, if `a` is greater than `b` and `a` is not divisible by `b`, then

```
gcd(a, b) = gcd(b, a % b)
```

Write the `gcd` function recursively using Euclid's algorithm.

```python
def gcd(a, b):
    """Returns the greatest common divisor of a and b.
    Should be implemented using recursion.

    >>> gcd(34, 19)
    1
    >>> gcd(39, 91)
    13
    >>> gcd(20, 30)
    10
    >>> gcd(40, 40)
    40
    """

    "*** YOUR CODE HERE ***"
    if a % b == 0:
        return b
    elif a > b and a % b != 0:
        return gcd(b, a % b)
    else:
        return gcd(b, a)
```

Use Ok to test your code:

```
python3 ok -q gcd
```

### Q2: Hailstone

For the `hailstone` function from [homework 1](https://inst.eecs.berkeley.edu/~cs61a/sp18/hw/hw01/#q5), you pick a positive integer `n` as the start. If `n` is even, divide it by 2. If `n` is odd, multiply it by 3 and add 1. Repeat this process until `n` is 1. Write a recursive version of hailstone that prints out the values of the sequence and returns the number of steps.

```python
def hailstone(n):
    """Print out the hailstone sequence starting at n, and return the
    number of elements in the sequence.

    >>> a = hailstone(10)
    10
    5
    16
    8
    4
    2
    1
    >>> a
    7
    """

    "*** YOUR CODE HERE ***"
    print(n)
    if n == 1:
        return 1
    elif n % 2 == 0:
        return hailstone(n // 2) + 1
    else:
        return hailstone(3 * n + 1) + 1
```

Use Ok to test your code:

```
python3 ok -q hailstone
```

# Midterm Review

**Note**: The following questions are in [lab03_extra.py](https://inst.eecs.berkeley.edu/~cs61a/sp18/lab/lab03/lab03_extra.py).

## Functions

### Q3: WWPD: Call Expressions

> Use Ok to test your knowledge with the following "What Would Python Display?" questions:
>
> ```
> python3 ok -q call_expressions -u
> ```
>
> For all WWPD questions, type `Function` if you believe the answer is `<function...>`, > `Error` if it errors, and `Nothing` if nothing is displayed.

```python
>>> from operator import add
>>> def double(x):
...     return x + x
...
>>> def square(y):
...     return y * y
...
>>> def f(z):
...     add(square(double(z)), 1)
...
>>> f(4)
Nothing
______
```

```python
>>> def foo(x, y):
...     print("x or y")
...     return x or y
...
>>> a = foo
Nothing
______
>>> b = foo()
Error
______
>>> c = a(print("x"), print("y"))
x
y
x or y
______
>>> print(c)
None
______
```

```python
>>> def welcome():
...     print('welcome to')
...     return 'hello'
...
>>> def cs61a():
...     print('cs61a')
...     return 'world'
...
>>> print(welcome(), cs61a())
welcome to
cs61a
hello world
______
```

## Higher Order Functions

### Q4: I Heard You Liked Functions...

Define a function `cycle` that takes in three functions `f1`, `f2`, `f3`, as arguments. `cycle` will return another function that should take in an integer argument `n` and return another function. That final function should take in an argument `x` and cycle through applying `f1`, `f2`, and `f3` to `x`, depending on what `n` was. Here's what the final function should do to `x` for a few values of `n`:

- `n = 0`, return `x`
- `n = 1`, apply `f1` to `x`, or return `f1(x)`
- `n = 2`, apply `f1` to `x` and then `f2` to the result of that, or return `f2(f1(x))`
- `n = 3`, apply `f1` to `x`, `f2` to the result of applying `f1`, and then `f3` to the result of applying `f2`, or `f3(f2(f1(x)))`
- `n = 4`, start the cycle again applying `f1`, then `f2`, then `f3`, then `f1` again, or `f1(f3(f2(f1(x))))`
- And so forth.

*Hint*: most of the work goes inside the most nested function.

```python
def cycle(f1, f2, f3):
    """Returns a function that is itself a higher-order function.

    >>> def add1(x):
    ...     return x + 1
    >>> def times2(x):
    ...     return x * 2
    >>> def add3(x):
    ...     return x + 3
    >>> my_cycle = cycle(add1, times2, add3)
    >>> identity = my_cycle(0)
    >>> identity(5)
    5
    >>> add_one_then_double = my_cycle(2)
    >>> add_one_then_double(1)
    4
    >>> do_all_functions = my_cycle(3)
    >>> do_all_functions(2)
    9
    >>> do_more_than_a_cycle = my_cycle(4)
    >>> do_more_than_a_cycle(2)
    10
    >>> do_two_cycles = my_cycle(6)
    >>> do_two_cycles(1)
    19
    """

    "*** YOUR CODE HERE ***"
    def g(n):
        def h(x):
            if n == 0:
                return x
            elif n == 1:
                return f1(x)
            elif n == 2:
                return f2(f1(x))
            elif n == 3:
                return f3(f2(f1(x)))
            else:
                return g(n - 3)(f3(f2(f1(x))))
        return h
    return g
```

Use Ok to test your code:

```
python3 ok -q cycle
```

## Lambda expressions

### Q5: Palindrome

A number is considered a palindrome if it reads the same forwards and backwards. Fill in the blanks '_' to help determine if a number is a palindrome. In the spirit of exam style questions, please do not edit any parts of the function other than the blanks.

```python
def is_palindrome(n):
    """
    Fill in the blanks '_____' to check if a number
    is a palindrome.

    >>> is_palindrome(12321)
    True
    >>> is_palindrome(42)
    False
    >>> is_palindrome(2015)
    False
    >>> is_palindrome(55)
    True
    """
    x, y = n, 0

    f = lambda: _____
    while x > 0:

        x, y = _____, f()
    return y == n
   "************code********" 
    x, y = n, 0
    f = lambda: 10 * y + x % 10
    while x > 0:
        x, y = x // 10 , f()
    return y == n
```

Use Ok to test your code:

```
python3 ok -q is_palindrome
```

## Environment diagrams

### Q6: Doge

Draw the environment diagram for the following code.

```python
wow = 6

def much(wow):
    if much == wow:
        such = lambda wow: 5
        def wow():
            return such
        return wow
    such = lambda wow: 4
    return wow()

wow = much(much(much))(wow)
```

Verify your solution with [Python Tutor](https://goo.gl/rLDpDe).

## More Recursion Practice

### Q7: Find the Bug

Find the bug with this recursive function.

```python
def skip_mul(n):
    """Return the product of n * (n - 2) * (n - 4) * ...

    >>> skip_mul(5) # 5 * 3 * 1
    15
    >>> skip_mul(8) # 8 * 6 * 4 * 2
    384
    """
    if n == 2:
        return 2
    else:
        return n * skip_mul(n - 2)
    "*************solution************"
    if n == 2:
        return 2
    elif n == 1:
        return 1
    else:
        return n * skip_mul(n - 2)
```

When you find it, run this to check your answer:

```
python3 ok -q skip_mul_ok -u
```

Then, fix the code in `lab03_extra.py` and run this to check your code:

```
python3 ok -q skip_mul
```

### Q8: Is Prime

Write a function `is_prime` that takes a single argument `n` and returns `True` if `n` is a prime number and `False` otherwise. Assume `n > 1`. We implemented this in [Discussion 1](https://inst.eecs.berkeley.edu/~cs61a/sp18/disc/disc01.pdf) iteratively, now time to do it recursively!

> *Hint*: You will need a helper function! Remember helper functions are useful if you need to keep track of more variables than the given parameters, or if you need to change the value of the input.

```python
def is_prime(n):
    """Returns True if n is a prime number and False otherwise.

    >>> is_prime(2)
    True
    >>> is_prime(16)
    False
    >>> is_prime(521)
    True
    """

    "*** YOUR CODE HERE ***"
    def check(i):
        if i == n:
            return True
        elif n % i == 0:
            return False
        else:
            return check(i + 1)
    return check(2)
```

Use Ok to test your code:

```
python3 ok -q is_prime
```

### Q9: Interleaved Sum

Recall that the `summation` function computes the sum of a sequence of terms from 1 to `n`:

```
def summation(n, term):
    """Return the sum of the first n terms of a sequence.

    >>> summation(5, lambda x: pow(x, 3))
    225
    """
    total, k = 0, 1
    while k <= n:
        total, k = total + term(k), k + 1
    return total
```

Write a function `interleaved_sum` that similarly computes the sum of a sequence of terms from 1 to `n`, but uses different functions to compute the terms for odd and even numbers. Do so without using any loops or testing in any way if a number is odd or even. (You may test if a number is equal to 0, 1, or `n`.)

> *Hint*: Use recursion and a helper function!

```python
def interleaved_sum(n, odd_term, even_term):
    """Compute the sum odd_term(1) + even_term(2) + odd_term(3) + ..., up
    to n.

    >>> # 1 + 2^2 + 3 + 4^2 + 5
    ... interleaved_sum(5, lambda x: x, lambda x: x*x)
    29
    """

    "*** YOUR CODE HERE ***"
    def help(total, count, is_even, odd_term, even_term):
        if count > n:
            return total
        elif is_even == 0:
            total += even_term(count)
        else:
            total += odd_term(count)
        return help(total, count + 1, 1-is_even, odd_term, even_term)
    return help(0, 1, 1, odd_term, even_term)
```

Use Ok to test your code:

```
python3 ok -q interleaved_sum
```

### Q10: Ten-pairs

Write a function that takes a positive integer `n` and returns the number of ten-pairs it contains. A ten-pair is a pairs of digits within `n` that sum to 10. *Do not use any assignment statements.*

The number 7,823,952 has 3 ten-pairs. The first and fourth digits sum to 7+3=10, the second and third digits sum to 8+2=10, and the second and last digit sum to 8+2=10:

> *Hint*: Use a helper function to calculate how many times a digit appears in n.

```python
def ten_pairs(n):
    """Return the number of ten-pairs within positive integer n.

    >>> ten_pairs(7823952)
    3
    >>> ten_pairs(55055)
    6
    >>> ten_pairs(9641469)
    6
    """

    "*** YOUR CODE HERE ***"
    if n < 10:
        return 0
    def help(n, target):
        if n == 0:
            return 0
        elif n % 10 + target == 10:
            return 1 + help(n // 10, target)
        else:
            return help(n // 10, target)
    return help(n // 10, n % 10) + ten_pairs(n // 10)
```

Use Ok to test your code:

```
python3 ok -q ten_pairs
```