---
title: "Containers"
weight: 2
authors: ["Vanshaj Singhania"]
---

Sometimes, you have a series of data that goes together but you're not exactly sure how to store it, short of having a number of different variables to represent each individual piece. That's a little chaotic, so there has to be a simpler way to store them!

## Lists
Python, and actually almost all programming languages, have a container functionality. In Python specifically, this functionality is called a `list`. Remember the Hog project? What if we wanted to store the results of rolling 5 dice?

```python
die_0 = 2
die_1 = 3
...
die_4 = 4
```

This would be extremely irritating if the number of dice was scaled to, say, a hundred. Instead, a `list` can contain all of these values.

```python
dice = [2, 3, 5, 6, 4]
```

Much nicer, isn't it? We can actually store virtually *anything* in a list, even other lists! Say you want to track an entire game. How would that look?

```python
three_rounds = [[2, 3], [1], [4, 6, 5]]
```

Yes, you can even store other lists inside lists.

## Accessing List Elements
Accessing lists can be weird if you've never done computer science before, because lists in most programming languages (including Python) are zero-indexed. This means that the elements of a list start at the index 0 and go up to size - 1.

```python
randoms = [2, 4, 3, 7, 1]
indices = [0, 1, 2, 3, 4]
```

Here, the `indices` list represents the indices of the `randoms` list (note that this is just to show what zero-indexing is). To access a specific element, we can simply do the following:

```python
>>> randoms = [2, 4, 3, 7, 1]
>>> randoms[0]
2
>>> randoms[4]
1
>>> randoms[5] # this throws an error. why?
```

Another handy thing we can do with a list is get its length using the `len` method:
```python
>>> len(randoms)
5
```

Note that the length of this list is still 5, not 4. This is because it does contain 5 elements, it's just that these elements are referred to starting at 0.

## Slicing
Sometimes, you only need a piece of a list. You can copy such a piece using list slicing, which looks something like this:

```python
>>> randoms[1:3]
[4, 3]
```

Here, `1` is the starting index, the first index to be included in the slice. On the other hand, `3` is the ending index, the index **after the last index** to be included. This means that the element at the ending index is not actually included in the slice. We can also leverage some Python defaults:

```python
>>> randoms[:2] # the default starting index is 0, so omitting it defaults to 0
[2, 4]          # also, the element at index 2 is not included!
>>> randoms[3:] # the default ending index is the length of the list, so omitting it defaults to that
[7, 1]          # note that when slicing, referring to the length of the list as the ending index is okay. why?
>>> randoms[:]  # if we omit both, this effectively just creates a copy of the whole list
[2, 4, 3, 7, 1]
```

One of the comments in that example was a question. If you didn't figure it out, that's okay! I'm here to give you the answers -- when you slice a list, the ending index effectively tells the interpreter to stop duplicating elements **right before this index.** This means that if you told the interpreter that the ending index is the length of the list, it wouldn't actually try to look into an element at that index. As such, we won't violate zero-indexing by using the length as our last index -- we'll just go all the way to the end in our slice!

## Digression: `for`
As promised in the `for` notes, I'm going to clarify everything that I left unclarified. Now that you know what a list is, it's a good time to tell you that the `<expression>` in a `for` loop is an *iterable*, which for now is anything you can iterate over. That is, something like a list which has multiple elements that you can go over one by one. This means that the `<expression>` part of a `for` loop is effectively a list for now, and when you create a `for` loop you're basically going over the elements of list one by one.

```python
>>> for i in [0, 1, 2]:
...     print(i)
0
1
2
```

First, the variable `i` is created. It is then bound to `0`, and the suite is executed. Then, `i` is rebound to `1` and the suite is executed. Then, `i` is rebound to `2` and the suite is executed. Lastly, we run out of elements to loop over and exit the loop.

## Ranges
So what does the mysterious `range` function we used in the `for` notes do? Well, it returns a list that you can iterate over! The way `range(x,y)` works is basically that it starts at `x` and creates a list all the way up to, but not including, `y`.

```python
>>> list(range(0, 2))
[0, 1]
>>> list(range(-2, 2))   # yes, we can start at negative indices
[-2, -1, 0, 1]
>>> list(range(2))       # if we omit the first argument, the range starts at 0
[0, 1]
>>> list(range(0, 4, 2)) # we can even skip elements. here, we return every other element
[0, 2]
```

Notice that we use a `list` wrapper for each of these calls. This is because there's an added layer of complexity over how `range` works, but we'll keep it slightly simpler for now. Back to lists.

## List Comprehensions
As with everything else in computer science, lists are only useful if you use them. Fortunately, Python even includes some ways to map or filter lists! You can apply some sort of function to every element in a list, and you can choose to select only certain elements based on some condition.

From Lab 5, the general syntax of list comprehensions is as such:
```python
[<expression> for <element> in <sequence> if <conditional>]
```

Also from Lab 5: the syntax is designed to read like English: "Compute the `<expression>` for each `<element>` in the `<sequence>` if the `<conditional>` is true for that element." What does this mean?

Let's do this piece by piece. Say we have the following:
```python
def expression(x):
    return x + 1

sequence = [1, 2, 3]
```

### `for`
Now, if you recall from `for` loops, we can create a variable and bind it one by one to each element in a sequence.

```python
>>> [expression(x) for x in sequence]
[2, 3, 4]
```

This code tells Python, in a short-handed way, that for each `x` in `sequence`, apply `expression(x)` and create a list of the results. This is technically equivalent to the following:

```python
>>> result = []
>>> for x in sequence:
...     result = result + expression(x)
>>> result
[2, 3, 4]
```

Though I'm sure you see why the 1-line approach might be favored over the 4-line approach.

### `if`
There's another aspect to these comprehensions: the optional `if`. This is what does the filtering.

```python
>>> [expression(x) for x in sequence if x % 2 == 1]
[2, 4]
```

The way this is applied is that the original list if first truncated to remove all elements that don't meet the `if` condition. In this case, we convert the list `[1, 2, 3]` to a list containing only the elements that are not divisible by 2. This leaves us with `[1, 3]`, which is then used to replace the `sequence`. The new call becomes:

```python
>>> [expression(x) for x in [1, 3]]
[2, 4]
```

This we already know how to understand.

### Full Equivalents
This whole clause is a simplification of the following code:

```python
>>> result = []
>>> for x in sequence:
...     if x % 2 == 1
...         result = result + expression(x)
>>> result
[2, 4]
```

A further unsimplification might be to get rid of the `expression` and `sequence` variables.

```python
>>> result = []
>>> for x in [1, 2, 3]:
...     if x % 2 == 1
...         result = result + (x + 1)
>>> result
[2, 4]
```

All of these do the same thing, but which one would you prefer?