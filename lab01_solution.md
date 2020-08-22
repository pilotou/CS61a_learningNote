# Lab 1: Expressions and Control Structures



## What Would Python Display (Part 1)?

### Q1: WWPD: Veritasiness

> Use Ok to test your knowledge with the following "What Would Python Display?" questions:
>
> ```
> python3 ok -q short_circuiting -u
> ```

```python
>>> True and 13

______
>>> False or 0

______
>>> not 10

______
>>> not None

______
```

```python
>>> True and 1 / 0 and False

______
>>> True or 1 / 0 or False

______
>>> True and 0

______
>>> False or 1

______
>>> 1 and 3 and 6 and 10 and 15

______
>>> 0 or False or 2 or 1 / 0

______
```

```python
>>> not 0

______
>>> (1 + 1) and 1

______
>>> 1/0 or True

______
>>> (True or False) and False

______
```

### Q2: WWPD: Loops

> Use Ok to test your knowledge with the following "What Would Python Display?" questions:
>
> ```
> python3 ok -q loops -u
> ```

```python
>>> n = 3
>>> while n >= 0:
...     n -= 1
...     print(n)

______
```

> *Hint*: Make sure your `while` loop conditions eventually evaluate to a false value, or they'll never stop! Typing `Ctrl-C` will stop infinite loops in the interpreter.

```python
>>> n = 4
>>> while n > 0:
...     n += 1
...     print(n)

______
```

```python
>>> def go(n):
...     if n % 2 != 0:
...         print(n / 2)
...         return
...     while n > 0:
...         print(n)
...         n = n // 2
>>> go(4)

______
>>> go(5)

______
```

```python
>>> zero = 2
>>> while zero != 0:
...    zero = zero // 2
...    print(zero)

______
>>> positive = 28
>>> while positive:
...    print("positive?")
...    positive -= 3

______
>>> positive = -9
>>> negative = -12
>>> while negative:
...    if positive:
...        print(negative)
...    positive += 3
...    negative += 3

______
```

### Q3: Repeated

Implement the `repeated` function, which takes a one-argument function `f`, a positive integer `n`, and a parameter `x`. It returns the result of *composing*, or applying, `f` `n` times on `x`, i.e., `f(f(...f(x)...))`.

```python
def repeated(f, n, x):
    """Returns the result of composing f n times on x.

    >>> def square(x):
    ...     return x * x
    ...
    >>> repeated(square, 2, 3)  # square(square(3)), or 3 ** 4
    81
    >>> repeated(square, 1, 4)  # square(4)
    16
    >>> repeated(square, 6, 2)  # big number
    18446744073709551616
    >>> def opposite(b):
    ...     return not b
    ...
    >>> repeated(opposite, 4, True)
    True
    >>> repeated(opposite, 5, True)
    False
    >>> repeated(opposite, 631, 1)
    False
    >>> repeated(opposite, 3, 0)
    True
    """

    "*** YOUR CODE HERE ***"
    k = 0
    while k < n:
        k = k+1
        x = f(x)
    return x
```

Use Ok to test your code:

```
python3 ok -q repeated
```

### Q4: Sum Digits

Write a function that takes in a nonnegative integer and sums its digits. (Using floor division and modulo might be helpful here!)

```python
def sum_digits(n):
    """Sum all the digits of n.

    >>> sum_digits(10) # 1 + 0 = 1
    1
    >>> sum_digits(4224) # 4 + 2 + 2 + 4 = 12
    12
    >>> sum_digits(1234567890)
    45
    """

    "*** YOUR CODE HERE ***"
    total = 0
    while n > 0:
        n, last = n // 10, n % 10
        total = total + last
        return total       
```

Use Ok to test your code:

```
python3 ok -q sum_digits
```

### Q5: Double Eights

Write a function that takes in a number and determines if the digits contain two adjacent 8s.

```python
def double_eights(n):
    """Return true if n has two eights in a row.
    >>> double_eights(8)
    False
    >>> double_eights(88)
    True
    >>> double_eights(2882)
    True
    >>> double_eights(880088)
    True
    >>> double_eights(12345)
    False
    >>> double_eights(80808080)
    False
    """

    "*** YOUR CODE HERE ***"
    just_saw_an_eight =False
    while n>0:
        n,last = n//10, n%10
        if last == 8 and just_saw_an eight:
            return True
        if last == 8:
            just_saw_an_eight = True
        else:
            just_saw_an_eight = False
    return False
	"""my code
	while n > 0:
        last = n % 10
        n = n // 10
        if last == 8:
            return n % 10 == 8
    return False
	"""
```

Use Ok to test your code:

```
python3 ok -q double_eights
```

# Optional Questions

## What Would Python Display (Part 2)?

### Q6: WWPD: Truthiness

> Use Ok to test your knowledge with the following "What Would Python Display?" questions:
>
> ```
> python3 ok -q truthiness -u
> ```

```python
>>> 0 or True

True
>>> not '' or not 0 and False

True
>>> 13 and False

False
```

```python
>>> False or 1

1
>>> '' or 1 and 1/0

error
>>> not 0 and 12 or 0

12
```

### Q7: WWPD: What If?

> Use Ok to test your knowledge with the following "What Would Python Display?" questions:
>
> ```
> python ok -q what_if -u
> ```

The functions below are already defined in `lab01.py`. If you get stuck, try `python -i lab01_extra.py` and experiment.

> **Hint**: `print` (unlike `return`) does *not* cause the function to exit!

```python
>>> def xk(c, d):
...     if c == 4:
...         return 6
...     elif d >= 4:
...         return 6 + 7 + c
...     else:
...         return 25
>>> xk(10, 10)

23
>>> xk(10, 6)

23
>>> xk(4, 6)

6
>>> xk(0, 0)

25
```

```python
>>> def how_big(x):
...     if x > 10:
...         print('huge')
...     elif x > 5:
...         return 'big'
...     elif x > 0:
...         print('small')
...     else:
...         print("nothin'")
>>> how_big(7)

'big'
>>> how_big(12)

huge
>>> how_big(1)

small
>>> how_big(-1)

nothin'
```

```python
>>> def so_big(x):
...     if x > 10:
...         print('huge')
...     if x > 5:
...         return 'big'
...     if x > 0:
...         print('small')
...     print("nothin'")
>>> so_big(7)

'big'
>>> so_big(12)

huge
'big'
>>> so_big(1)

small
nothin'
```

```python
>>> def ab(c, d):
...     if c > 5:
...         print(c)
...     elif c > 7:
...         print(d)
...     print('foo')
>>> ab(10, 20)

10
'foo'
```

```python
>>> def bake(cake, make):
...     if cake == 0:
...         cake = cake + 1
...         print(cake)
...     if cake == 1:
...         print(make)
...     else:
...         return cake
...     return make
>>> bake(0, 29)

1
29
29
>>> bake(1, "mashed potatoes")

mashed potatoes
'mashed potatoes'
```

## More Coding Practice

### Q8: Fix the Bug

The following snippet of code doesn't work! Figure out what is wrong and fix the bugs.

```python
def both_positive(x, y):
    """Returns True if both x and y are positive.

    >>> both_positive(-1, 1)
    False
    >>> both_positive(1, 1)
    True
    """

    return x and y > 0 # You can replace this line!
	"""
	answer:
	return x > 0 and y > 0
	"""
```

Use Ok to test your code:

```
python ok -q both_positive
```

### Q9: Falling Factorial

Let's write a function `falling`, which is a "falling" factorial that takes two arguments, `n` and `k`, and returns the product of `k` consecutive numbers, starting from `n` and working downwards.

```python
def falling(n, k):
    """Compute the falling factorial of n to depth k.

    >>> falling(6, 3)  # 6 * 5 * 4
    120
    >>> falling(4, 0)
    1
    >>> falling(4, 3)  # 4 * 3 * 2
    24
    >>> falling(4, 1)  # 4
    4
    """

    "*** YOUR CODE HERE ***"
    fa = 1
    while k > 0:
    	fa = n * fa
        n -= 1
        k -= 1
    return fa
```

Use Ok to test your code:

```
python ok -q falling
```

## I Want to Play a Game

Now that you have learned about call expressions and control structures, you can code an algorithm! An algorithm is a set of steps to accomplish a task. You use algorithms every day -- from adding numbers by hand to getting to your next lecture.

Let's play a number guessing game with Python! Pick a number and Python will guess randomly until it guesses correctly.

All the code for this guessing game will be in `lab01_extra.py`. In your terminal, start an interactive session with Python:

```
python -i lab01_extra.py
```

The `guess_random` function will prompt you for a number, ask if its guess is correct (many times) and return the number of guesses Python had to make. To tell Python if its guess is correct, just enter `y` at the `[y/n]` prompt. If it's wrong, enter `n`. Python isn't very good at guessing yet, so if it's taking too long, you can type `Ctrl-C` to make it stop.

```
>>> guess_random()
Pick an integer between 1 and 10 (inclusive) for me to guess: 7
Is 1 your number? [y/n] n
Is 5 your number? [y/n] n
...
```

Randomly guessing works, but you can create an even better guessing strategy.

### Q10: Guess Linear

One weakness in the `guess_random` strategy is that it can repeat (incorrect) guesses. Rather than guessing wildly, let's guess numbers in increasing order.

> Note: `is_correct` is a function that will ask the user if the guess is correct and return `True` if the user confirms that the guess matches the correct number. Feel free to reference the implementation of `guess_random` as you implement `guess_linear`.

```python
def guess_linear():
    """Guess in increasing order and return the number of guesses."""
    prompt_for_number(LOWER, UPPER)
    num_guesses = 1
    guess = LOWER

    "*** YOUR CODE HERE ***"
    while not is_correct(guess):
        guess += 1
        num_guesses += 1
    return num_guesses
```

The best way to test this function is by playing with it interactively. See if your algorithm does what you expect!

### Q11: Guess Binary

**Challenge question.** The `guess_linear` function can take a long time if your number is large. However, a strategy called *binary search* can find the correct number faster. The idea is to start in the middle of the range and after each incorrect guess ask if the guess `is_too_high` or too low. Either way, you can eliminate half the remaining possible guesses.

> *Hint*: Try using the `is_too_high` function to implement a faster strategy. `is_too_high` will return `True` if the guess is greater than the correct number.
>
> ```
> >>> result = is_too_high(5)
> Is 5 too high? [y/n] y
> >>> result
> True
> ```

> *Hint*: You may want to update other variables besides `guess`.

```python
def guess_binary():
    """Return the number of attempted guesses. Implement a faster search
    algorithm that asks the user whether a guess is less than or greater than
    the correct number.

    Hint: If you know the guess is greater than the correct number, then your
    algorithm doesn't need to try numbers that are greater than guess.
    """
    prompt_for_number(LOWER, UPPER)
    num_guesses = 1
    lower, upper = LOWER, UPPER
    guess = (lower + upper) // 2

    "*** YOUR CODE HERE ***"
    while not is_correct(guess):
        if is_too_high(guess):
            upper = guess - 1
        else:
            lower = guess + 1
        guess = (lower + upper) // 2
        num_guesses += 1
    return num_guesses
```

If you choose a number between 1 and 10, this approach should need no more than 4 guesses to find your number.

The best way to test this function is by playing it interactively. Try to think of *edge cases* -- numbers that might cause your algorithm to do the wrong thing. If you edit the Python file while running it interactively, you will need to `exit()` and restart the interpreter in order for those changes to take effect.

So far, your algorithms have only had to find a number between 1 and 10. What if we expanded the possible range of numbers to be between 1 and 100? How many guesses would each algorithm make if you picked 100 to be your number?

### A Second Look

Let's try to visualize the two algorithms you've just written! We've provided code that will run each algorithm 1000 times and plot the number of guesses the algorithms had to make. The numbers are randomly chosen from between 1 and 100.

```
python guessing_game_graph.py guess_linear
python guessing_game_graph.py guess_binary
```

Each bar represents the number of guesses the algorithm took to find the correct number. The height of each bar represents the frequency of each number of guesses. Look carefully at the axes when comparing the two graphs! You should see that `guess_linear` sometimes took up to 100 guesses; what was the highest number of guesses that `guess_binary` took?

You can see our plots for [guess_linear](https://chart.googleapis.com/chart?cht=bvg&chtt=guess_linear&chxt=x,y,x,y&chs=500x500&chd=t:4,23,32,39,48,60,66,75,82,93,102,113,125,140,157,165,176,187,196,204,215,223,234,243,251,257,273,287,297,306,315,322,327,339,352,362,371,384,394,399,415,420,433,445,451,460,473,486,492,503,511,516,521,534,543,551,560,568,579,593,599,608,619,630,642,655,671,685,698,706,719,725,730,741,754,772,783,795,800,809,818,824,829,842,845,855,866,878,882,897,908,914,924,935,946,960,968,979,994,1000&chxl=0:|0|10|20|30|40|50|60|70|80|90|100|2:|Max%20number%20of%20guesses|3:|Frequency|&chxp=0,0|2,50|3,500&chds=a&chco=3072F3&chbh=a&chm=s,000000,0,-1,5|s,000000,1,-1,5&chdlp=l) and [guess_binary](https://chart.googleapis.com/chart?cht=bvg&chtt=guess_binary&chxt=x,y,x,y&chs=500x500&chd=t:10,27,79,176,329,644,1000&chxl=0:|1|2|3|4|5|6|7|2:|Max%20number%20of%20guesses|3:|Frequency|&chxp=0,8,22,36,50,64,78,92|2,50|3,500.0&chds=a&chco=3072F3&chbh=a&chm=s,000000,0,-1,5|s,000000,1,-1,5&chdlp=l). If your plots only have one bar, make sure your functions are returning the correct number of guesses!