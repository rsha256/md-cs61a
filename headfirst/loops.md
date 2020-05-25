---
title: "Loops"
weight: 3
authors: ["Vanshaj Singhania"]
---

We learned about conditions and saw how we can use them to make our code run only when we want it to. What if we wanted to do something over and over until a condition was met? For example, what if we wanted to count down from 5?

## Brute Force

We could do this:
```python
print(5)
print(4)
print(3)
print(2)
print(1)
print(0)
```

We could also do this:
```python
def print_sub(x):
    print(x)
    return x - 1

x = 5
x = print_sub(x)    # prints 5
x = print_sub(x)    # prints 4
x = print_sub(x)    # prints 3
x = print_sub(x)    # prints 2
x = print_sub(x)    # prints 1
print_sub(x)        # prints 0
```
Where we discard the last return value, since we don't care for it anymore.

These two approaches have one thing in common: we can't use them if `x` becomes too big, or we'll have too many lines. In fact, this approach would *never* work if `x` was arbitrary; if we ever got around to accomodating user input, we'd need an infinite amount of lines to make sure that we count down correctly. This is called the *brute force* solution, where you hard-code every step of the process.

Evidently, this isn't the most elegant way of doing things. What's the alternative?

## `while` Loops
If you think about the problem, you'll notice that we essentially want to print our `x`s in a loop until we get to 0. Surely there has to be a way to do this for an arbitrary `x`! The answer is a `while` loop, which looks a little something like this:

```python
x = 5

while x > -1:
    print(x)
    x = x - 1
```

And that's it! We can now make `x` whatever we want, and the rest of our code doesn't change! What this loop does is as long as `x > -1` is true (meaning the last possible value for `x` is `0`), we do what's inside the loop: print `x`, and set `x` to `x - 1` (otherwise known as *decrementing* `x`). We continue to print and decrement `x` until it's no longer greater than `-1`, which occurs after `x = 0`, since we then set it to `x = 0 - 1`.

This loop alone gives programming a ridiculous amount of power. Say we're given an arbitrary `x` and now, instead of counting down, we want to find it's greatest divisor (i.e. we want to find `y` such that `x / y` has no remainder). How do we do this using a `while` loop?

Recall that there exists a variety of division operators. We're particularly concerned with the modulo (`x % y`) operator here, which gives us the remainder of dividing `x` by `y`. We essentially want to start at `y = x - 1` (since `y = x` of course divides `x`) and work down until we find a value for `y` such that `x % y = 0`. Give it a try on your own before peeking at a solution below!

```python
x = 6
y = x - 1

while x % y != 0:
    y = y - 1

print(y)
```

The result, as expected by inspection, is `3`. But wait, isn't there a way we can simplify our `while` condition? Recall that `0` is a falsey value, which means that our loop essentially repeats for as long as `x % y` is a truthy value. Let's simplify our condition then:

```python
x = 6
y = x - 1

while x % y:
    y = y - 1

print(y)
```

The result is the same.

## The `not` Keyword
Now that we've gotten through a basic understanding of `while` loops, I want to quickly touch on a simple yet powerful keyword in Python: `not`. The purpose of this operator is to negate the condition it's applied to. For example:

- `not True` is `False`
- `not False` is `True`
- `not x` is the opposite of `x`

The last bit is especially useful. Say now that instead of finding the greatest divisor, we want to find the smallest number than *doesn't* evenly divide `x`. We can write this like so:

```python
x = 6
y = 1

while x % y == 0:
    y = y + 1

print(y)
```

We know that `x` is divisible in this case by 1, 2, and 3, so the result here is `4`. Let's use the `not` operator to simplify the `while` condition:

```python
x = 6
y = 1

while not x % y:
    y = y + 1

print(y)
```

We loop as long as `x % y` is not a truthy value, which is as long as it evaluates to `0`.
