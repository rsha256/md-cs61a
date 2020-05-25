---
title: "Lambdas"
weight: 4
authors: ["Vanshaj Singhania"]
---

Let's take a break from all this new condition and loop stuff and go back to something we recognize: functions. Remember these?

```python
def hello():
    print("world!")
```

Simple one-line functions like these are pretty common (though typically they'll do something more important, like a quick computation). Equally common are one-line functions with one or two arguments, like so:

```python
def add_2(x):
    return x + 2

x = add_2(2)    # sets x to 4
```

For such short functions, it feels like a waste to dedicate two whole lines to define it. That's what lambdas are for!

## Syntax
The Python lambda function is a one-line function that evaluates and returns its only line of content. The syntax looks like this:

```python
function_name = lambda x, y, z: x + y + z
```

Where `function_name` is the optional name to assign the lambda to (you'll see why it's optional [soon](#anonymous-functions)), `lambda` is the keyword to make a lambda function, `x, y, z` are the optional arguments (you could have a no-argument lambda function), and `x + y + z` is an expression that can be evaluated and returned.

That's a lot to process, so let's see some examples.

## Usage
Note that a lambda function is, at the end of the day, a function. To make things easier to understand, I'm going to write lambda functions with their traditional equivalent.

Let's start with a function with no arguments:
```python
def hello():
    return "world!"

hello = lambda: "world!"
```

To call this function, you would write `hello()`. It's a function with no arguments!

Let's see a function with one argument:
```python
def add_2(x):
    return x + 2

add_2 = lambda x: x + 2
```

To call this function, you would write (for example) `add_2(4)`. The result in both cases would be `6`.

## Anonymous Functions
Sometimes you want to create a function on the fly and don't really need to give it a name. Let's take the `add_2` function, for example; if we only need that function once, then giving it a name isn't necessary. It's convenient, for sure, but it'll just end up taking unnecessary space on our computer.

Instead, we can define a lambda function *anonymously* and use it exactly once:

```python
(lambda x: x + 2)(4)
```

This will evaluate to `6`. Let's quickly break down what happened here: we first made a lambda function, `lambda x: x + 2`. We didn't give this a name, but when Python evaluated our complete expression, it automatically replaced our lambda with an anonymous function which could be called with one argument. We then called this function on one argument: `4`.

Think of it this way: we can do this:

```python
>>> 4 + 2
6
```

Or we can do this:

```python
>>> x = 4
>>> x + 2
6
```

The result is the same whether we name the `4` or not. Similarly, we can use lambdas regardless of whether they're named or not. `add_2` represents the same thing as the `lambda` expression, just as `x` represents the same thing as `4`, so whether we assign these expressions to variables or not is always a choice, not an obligation.

Unless, of course, a test question requires that you give it a name. In that case, please give it a name :).
