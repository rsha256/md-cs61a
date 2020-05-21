---
title: "Conditions"
weight: 1
authors: ["Vanshaj Singhania"]
---

Most of the time, you only want your code to run if something is true (or false). For example, say you want to find the smaller of two numbers: if the first number is less than the second, then that's what you want to return. If the second is less than the first, then that's what you want to return. So how do you figure this out?

## Booleans
A boolean is a data type that represents one of two values: `True` or `False`. Its sole purpose is to designate whether a condition is met or not. In Python, you can define booleans as regular variables:

```python
this_is_true = True
this_is_false = False
```

Evidently, this isn't particularly useful. Simply assigning variables doesn't really help us very much, so why bother? Well, booleans become particularly handy when you can use them to control what part of your code is executed.

## `if` Statements
An `if` statement in any programming language checks whether the following condition is true. If it is, then the next few lines of code are executed. If it isn't, the next few lines are skipped.

Here's an example. Say your code looks like this:

```python
x = 1
y = 2

print(x)
print(y)
```

But say you only want to print one of `x` and `y`, depending on some condition. You could format your code to look like this:

```python
x = 1
y = 2

if True:
    print(x)
else:
    print(y)
```
What this does is it tells Python that if something is true, print `x`. Otherwise, print `y`.

Still not very useful though. `if True` will always be true, because `True` is true. How can we replace this with a condition that might *not* be true?

## Conditions
Remember how we wanted to find the smaller of two numbers? Well, we can use a familiar mathematical operator, `<`, to check! What does this mean?

```python
x = 1
y = 2

if x < y:
    print(x)
if y < x:
    print(y)
```

When you get to the `if` statement, Python will evaluate the condition you gave it: `x < y`. If this condition is true, then `x` will be printed. If it isn't true, then `y` will be printed because the next condition -- `y < x` -- is true. This is better -- we can use our code to do what we want, *when* we want it.

You can create conditions in many ways, the most typical being the following:

- `x < y` true if `x` is less than `y`
- `x > y` true if `x` is greater than `y`
- `x == y` true if `x` is equal to `y`
- `x <= y` true if `x` is less than or equal to `y`
- `x >= y` true if `x` is greater than or equal to `y`
- `x != y` true if `x` is not equal to `y`

## Truthy, Falsey
The idea behind conditions is a notion of *truthy* and *falsey* values. Truthy values are values that evaluate to `True`, and falsey values evaluate to `False`. For each condition that I listed above, if the condition is true, then we have a truthy value. If it isn't, then we have a falsey value.

This is sort of different from the general notion of `True` and `False`, because you could sometimes see code like this:

```python
if x:
    print(x)
```

What does this do? How is this a valid condition? There's actually a number of ways this would work:
- `x` could be a condition like `x = 1 < 2`, which evaluates to `True`
- `x` could be a boolean like `x = False`, which evaluates to `False`
- `x` isn't either of these and is instead just a regular variable, like `x = 0` or `x = 'hi'`

In the last case, how do you determine whether `x` is truthy or falsey? It's actually quite straightforward: if `x` is a non-boolean variable, it is always truthy *except* when it's `0`, `''` (empty string), or `[]` (empty list).

Different languages do this differently, but this is the rundown of how Python handles truthy and falsey values.

## `if, else-if, else` Statements
We saw the `if` syntax above, which allows us to run code only if a certain condition is true. What if it isn't? We manually created the opposite condition in our quest to find the smaller of two numbers, but what happens if the two numbers are equal? Right now, nothing is printed, because neither condition is met!

We can solve this using an `else` clause. If we remove the second condition and replace it with `else`, our code looks like this:

```python
x = 1
y = 2

if x < y:
    print(x)
else:
    print(y)
```

What happens here is, if `x < y`, then we print `x`. Otherwise, regardless of whether `x == y` or `x > y`, we print `y`. Pretty neat!

But there's another catch. What if we actually wanted to print whether `x` was greater than, less than, or equal to `y`? Now, we'd have to handle the `==` case separately, but we don't have a way to handle three-way conditions!

Actually, we do. We can simply append `if` clauses to our statement to test for various conditions, like so:

```python
x = 1
y = 2

if x < y:
    print("Less than!")
    print(x)
else if x == y:
    print("Equal to!")
    print(x) # or y, doesn't matter!
else: # if is omiited, since at this point there is only 1 possibility
    print("Greater than!)
    print(y)
```

Much better, isn't it? We can easily chain conditions to create exhaustive conditions, which gives our code an extra edge by allowing it to do much more than previously possible.

To recap, here's what an `if` statement can look like:

```python
if <expression1>:
    <exp1 suite>
[else if <expression2>:] # repeated as many
[   <exp2 suite>       ] # times as you wish.
[else:                 ] # both else if and
[   <else suite>       ] # else are optional.
```
