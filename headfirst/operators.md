---
title: "Conditional Operators"
weight: 2
authors: ["Vanshaj Singhania"]
---

Right now, we know how to use simple conditions in `if-else` statements. What if we wanted to check the opposite of a condition? What about chaining conditions?

## `not`
The purpose of this operator is to negate the condition it's applied to. For example:

- `not True` is `False`
- `not False` is `True`
- `not x` is the opposite of `x`

The last bit is especially useful. Say we want to print `y` if it's smaller than `x`. We can write this like so:

```python
x = 6
y = 1

if y < x:
    print(y)
```

Lexicographically, it might look nicer to put the `x` before the `y` (or, maybe that's a functional reason you want to do this). Let's use the `not` operator to flip the condition:

```python
x = 6
y = 1

if not x < y:
    print(y)
```

If `x` is not smaller than `y`, we print `y`. There's a very subtle difference between this statement and the one above: the first `if` statement only evaluates to true if `y` is smaller than `x`, but the second one also evaluates to true if `y` is *equal* to `x`. Of course, we can correct for this by using `x <= y` if we need to.

This wasn't a very functional example for the `not` operator, but hopefully you see how it can be applied to other (more useful) cases.

## `and`
What if you wanted to check whether `x` was in a certain range? You could do something like this:

```python
x = 5

if x > 1:
    if x < 10:
        print(x)
```

This looks a little clunky, because you've got an extra line dedicated to what should basically be one condition. Let's see how the `and` operator can combine these conditions:

```python
x = 5

if x > 1 and x < 10:
    print(x)
```

This will only run if *both* given conditions are true! A simpler and easier-to-read condition :). You can also add more than two conditions here. Say you want to prin `x` if it's in that range *unless* it's 4:

```python
x = 5

if x > 1 and x < 10 and x != 4:
    print(x)
```

{{% notice note %}}
Side Note: Python actually has a nice feature built-in for checking if a number is in a certain range: `if 1 < x < 10:`. This has a very algebraic feel to it, which should help you make more sense of it. Note that `and` is still useful for cases where you're not checking numerical conditions, but this could be a cool trick to know.
{{% /notice %}}

## `or`
Similar to the `and` operator, `or` is very straightforward: if you want to check whether *one* of two or more conditions is true, you can chain them using `or`:

```python
x = 5

if x == 1 or x == 4 or x == 7:
    print(x)
```

This is an odd condition, but it gets the point across: if `x` is any of `1`, `4`, or `7`, print it!

## Short-Circuiting
Think about these conditions logically. If someone asks you to do something only if `x` is greater than 1 and less than 10, and you're told that `x` is 0, do you need to check both of these conditions? You already know it's less than 1, so the first condition fails. The second one could be true, but it won't matter, so you save yourself some thinking and stop!

Similarly, say someone tells you to do something only if `x` if `1`, `4`, or `7`, and you're told that `x` is 1, do you need to check the other two conditions? You already know that `x` is `1`, so the first condition passes. The other two could be true or false, but it won't matter, so you again save yourself some thinking and stop.

Python does both of these too. This is known as short-circuiting: if the first of a sequence of conditions evaluates to a falsey value in an `and` clause, Python realizes that the rest of the condition is irrelevant and stops. If it evaluates to a truthy value in an `or` clause, Python realizes that the rest is irrelevant and stops checking.

In action, this is a little more complicated. If you just run these conditions on an interpreter without the `if`, you'll see what I mean:

```python
>>> x = 5
>>> x > 1 and x < 10:
True
>>> x or x < 10:
5
```

The first one makes sense: the condition is obviously `True`, so that's what gets printed. But why do you get back a `5` on the second condition?

Well, Python doesn't actually yield `True` or `False`. What happens is the expression is evaluated, and in an `or` statement the first true expression's evaluated result is printed. If all the statements are false, then the last expression's result is printed.

```python
>>> x = 0
>>> x < 0 or x:
0
```

Here, everything is a falsey value, so the evaluated result of the last one gets printed.

In an `and` statement, the order is the opposite: if everything is truthy, the last expression is printed. If not, the first falsey expression is printed.

The reason that with numerical expressions we see `True` or `False` is because those are the values these expressions evaluate to!

## `None`
Another unique result is when something is `None`: the Python interpreter doesn't print `None` results, so if something evaluates to `None`, it doesn't get printed.

```python
>>> None or 0
0
>>> 0 or None
>>> # nothing was printed!
```

Remember the `print` function? It prints whatever is passed in but it doesn't return anything -- it returns `None`. What if we use it in a condition?

```python
>>> print(5) or None
5
```

Note that this expression isn't truthy! The `5` gets printed by the call to `print`, and the `None` gets "printed" as the evaluated result of the condition!    
