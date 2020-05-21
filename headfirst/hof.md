---
title: "Higher Order Functions"
weight: 4
authors: ["Vanshaj Singhania"]
---

Remember the `add_2` function from the previous section on lambdas? What if we wanted to make a generic `add_x` function, where `x` is any arbitrary value?

I know this sounds ridiculous: why would you overcomplicate a simple `x + y` operation? Bear with me here -- the simplicity of this operation makes this section much easier to understand.

So yeah, say you wanted to make generic `add_x` functions. You could do this:

```python
add_0 = lambda x: x + 0
add_1 = lambda x: x + 1
...
add_9 = lambda x: x + 9
```

And so on. But that's a lot of repetition: we're typing `lambda x: x + ` every single time, and the only thing changing is the last letter. Now, as programmers, if we see repetition, the first thing that comes to find is a function. The whole point of a function is to reduce repetition, so what could we do here to reduce repetition?

*Make sure you have an open mind before reading on, because this bit gets a little stressful sometimes.*

What if we made a function that made other functions? It sounds absurd, but think about it: if we can have machines making machines, why not functions making functions? Especially if we need to make the same sort of function over and over?

## Traditional Higher-Order Functions

To start off a little simpler, let's switch back from lambdas to traditional functions:

```python
def add_0(x):
    return x + 0

def add_1(x):
    return x + 1

...
def add_9(x):
    return x + 9
```

Now we've got even more repetition, so it looks a little more logical to make a function to do the heavy lifting. Functions that make functions are called *higher-order functions*. The name comes from the idea that a generic function is a *first-order* function, but if you do something within that function that involves creating and returning another function, you've gone past that first order.

Here's what a higher-order function to make `add_x` would look like:

```python
def make_adder(x):
    def adder(y):
        return x + y
    return adder
```

An extremely important thing to note here is that the internal `adder` function is *not* executed. It is simply created as a variable inside of `make_adder` and then returned, but the code within it is not evaluated for correctness until you actually call the inner function.

When `adder` is returned, only the physical function is sent back to the caller, meaning the name is not seen by whatever called `make_adder`. This means that we could do something like this:

```python
add_0 = make_adder(0)
add_1 = make_adder(1)
...
add_9 = make_adder(9)
```

Still repetitive, of course, but now you're repeating your own function calls, rather than a built-in feature of Python.

## Higher-Order Lambdas
Just as we can replace one-line functions with lambdas, we can replace one-line higher-order functions with higher-order lambdas. A *one-line higher-order function*, in my vocabulary, is any function whose sole action is creating and returning a one-line function.

Let's go step by step. We'll start with converting the inner function to a lambda:

```python
def make_adder(x):
    return lambda y: x + y
```

This works the same way as the previous function we made. Since we now just have a one-line function, why can't we just collapse it into another lambda?

```python
make_adder = lambda x: lambda y: x + y
```

Voila! We've just collapsed a four-line function into one, and it still works the same way. This syntax is slightly confusing, so let's break it down: `x + y` is the expression to be evaluated; `lambda y: x + y` is the internal function which adds the parameter `y` to the variable `x`, which is already defined by the time this function is called; `lambda x: __________` is the outer function which makes the internal function and returns it.

You can try to visualize this by calling it:
```python
make_adder(2)   # the 2 is passed into the outer function as x,
                # and the resulting return value is essentially
                # lambda y: 2 + y
```

And we're now free to make all the `add_x` functions we want!

## Currying
Think of what we just did: we effectively just summed two numbers together! We held onto the inner function because we figured we might want to add `x` to something again later, but what if this wasn't the reason?

Say we're making a program with user interaction, and you ask the user for arguments to add together one by one. You don't get both the operands at the same time, so you store them one by one:

```python
one = # get the input somehow
two = # get the input somehow
print(one + two)
```

This works, but we could leverage higher-order functions too! Notice that just as we don't need to know what the argument to the inner function is to make the outer function, we don't need to know what the argument to the outer function is to assign it to a variable:

```python
one = # get the input somehow
adder = make_adder(one)
two = # get the input somehow
print(adder(two))
```

This looks like much more lines, but that's because we're talking about short functions like one-time addition. What if a user told us instead that they wanted to add 2 to a bunch of things? We'd now do the exact same thing as when we first made higher order functions, except we'd just use our new higher order function many many times.

Think of this:
```python
print(x + 2)
print(y + 2)
print(z + 2)
```

As opposed to this:
```python
print(adder(x))
print(adder(y))
print(adder(z))
```

Less repetition! We don't have to add 2 every time anymore, because we have a function that does it for us. For that matter, this could be *any* number, not just 2!

Here's the thing about currying: it's not for efficiency. Currying doesn't make your code any faster or slower, but it makes it more *readable* and organized. Imagine reading through a hundred statements that had `+ 2` in them, as opposed to reading a hundred statements calling the same function. You already know what this function does, so you don't even have to read the entire line to know what's going on.

Think about this on a significantly larger scale. See why it could be helpful?
