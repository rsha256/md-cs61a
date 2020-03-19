---
title: "Functions"
weight: 6
authors: ["Vanshaj Singhania"]
---

But what can you really do with all of these different expressions? If you combine them into functions, quite a bit.

## What are Functions?
As with algebra, a function is something that takes one or more inputs, does something with this input, and returns an output. Let's start with an example that takes no inputs:

$$
f() = 5
$$

This function always returns $5$. Let's see how we would implement this in Python:

```python
def f():
    return 5
```

We can use this function over and over:

```python
>>> f()
5
>>> y = f()
>>> y
5
>>> y = 6
>>> y
6
>>> f()
5
```

Notice that assigning `y` to `f()` will assign it to the *result* of calling `f()`, not the function itself. So, changing `y` to `6` doesn't change the return value of `f()`.

## Anatomy of a Function
Before we analyze the anatomy of a function, let's look at another one.

$$
g(x) = x + 2
$$

This function, in math, takes an input $x$ and returns $x+2$. In Python, this looks like:

```python
def g(x):
    return x + 2
```

We can use this as follows:

```python
>>> g(5)
7
>>> z = g(2)
>>> z
4
>>> z = 5
>>> z
5
>>> g(2)
4
>>> g(3)
5
```

Let's break down this function.

```python
def g(x):           # there's a function coming called `g` that takes one input `x`
    return x + 2    # `g` returns `x+2`
```

Note that a function can have more than one line, but only one return statement.

```python
def h(x):           # there's a function coming called `h` that takes one input `x`
    y = x + 2       # assign `y` to `x+2`
    return y        # `h` returns `y`
```

This function does that exact same thing as `g`, but it first assigns `x+2` to a new variable before returning that new variable.

## Some Built-in Functions
Python comes with a number of functions that you may find useful. We'll discover more later, but here's a few.

```python
>>> print('Hello!')        # print the value inside the parentheses, without quotes.
Hello!
>>> print(print('Hello!')) # see the next section to understand how this is evaluated.
Hello!                     # the `print` function prints the input...
None                       # ...but note that it returns None, which is a representation of nothing.
>>> min(2, 5)              # return the minimum of two or more numbers, separated by commas.
2
>>> max(2, 5)              # return the maximum of two or more numbers, separated by commas.
5
```

## Evaluation
The way a function is evaluated is key to understanding how it works. Essentially, Python tries to evaluate every operand before evaluating the operator. In `h(x)`, `h` is the operator and `x` is the operand.

We'll use the functions `add` and `mul` for this example, so you can see a PEMDAS-style operation. These functions are in the `operator` package, which you'll learn about in a later week. For now, ignore the `import` statement in the example below.

```python
>>> from operator import mul, add
>>> add(5, mul(add(5, 2), 4))
33
```

So what happened here?

- Well, Python tried to evaluate `5`, then `mul(add(5, 2), 4)`.
  - In evaluating the second expression, Python tried to evaluate `add(5, 2)` and `4`.
     - In evaluating the first expression, Python tried to evaluate `5` and `2`.
     - Those were already evaluated, so the innermost `add` function executed and returned `7`.
  - Now, the `mul` function's parameters became `7` and `4`, so the `mul` function executed and returned `28`.
- Lastly, the outermost `add` function's parameters became `5` and `28`, so the function executed and returned `33`.