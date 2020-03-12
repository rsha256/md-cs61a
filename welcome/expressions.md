---
title: "Expressions & Names"
date: 2020-02-15T23:26:58-08:00
---

We'll start off a little slow and talk about expressions in python. From your math classes, you probably know that an expression is anything that can be evaluated, like `24+3`, `5/2`, `6.72`, etc..

In Python, expressions are pretty much the same -- anything that can be evaluated.

## Primitive Expressions
Primitive values in Python include numbers and booleans, which evaluate to themselves. Generally, anything that evaluates to itself in one step is a primitive expression.

```python
>>> 27
27
>>> False
False
>>> 4.27
4.27
```

Each of these is a primitive expression, as no computation is required to evaluate them.

## Arithmetic Expressions
This is just math! Python comes with the four basic arithmetic operators -- `+`, `-`, `*`, `/` -- as well as a few more than you'll find useful in your CS experience.

- `**`: this is the exponentiation operator; the equivalent of $2^2$ in Python is `2**2`.
- `//`: this is the floor division operator; it will round down the result of division and return an integer.
- `%`: this is the modulo operator; it will evaluate to the positive remainder from division.

{{% notice note %}}
The regular division operator returns a floating-point number, even if the numbers divide evenly. For example, `3/3` will return `1.`, not `1`. See the difference?\
\
On the other hand, the floor division and modulo operators will return integers.
{{% /notice %}}

Python also respects PEMDAS.

```python
>>> 3 + 2
5
>>> 3 % 2
1
>>> 3 / 2
1.5
>>> 3 // 2          # floor division rounds down!
1
>>> (3 + 2) / 5
1.0
>>> 6 % 4           # the positive remainder of 6/4
2
```

## Names
In Python, as with any other programming language, you can assign values to variable names. This allows to reuse and update values as your code executes, giving you more flexibility and functionality.

Assigning a variable is as simple as setting it equal to the result of an expression:

```python
>>> c = 5 + 2
>>> c
7
```

An important note made in Lab 0 that I'd like to reiterate here is that names are bound to **values**, not **expressions**. The statement above will first evaluate `5 + 2 = 7` and then set `c = 7`.