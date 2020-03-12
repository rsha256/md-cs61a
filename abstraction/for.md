---
title: "For Statements"
date: 2020-02-19T23:41:51-08:00
---

So far, if we had to iterate over something, we used `while` statements. As it turns out, Python actually has another type of iteration: `for` statements. Here's an example:

```python
>>> for i in range(0, 5):
...     print(i)
0
1
2
3
4
```

Let's break down what happens here. The `i` in the `for` statement tells Python to create a new variable in the current environment and bind it to the first value in the `range`. What `range` does will be more clear after reading the Containers notes after this, but for now, just keep in mind that `range(x,y)` returns the values `x`, `x+1`, all the way to `y-1` one by one.

What happens next is that we use the value of `i`, which is first set to `0`, inside our loop in the `print` statement. Then, we go back to the `for` statement and `i` gets set to the next value -- 1. This continues until `i` reaches 4. After this is printed, we return to the `for ` statement, but the `range` statement refuses to return anything because it's designed to not include the `y` index that's passed in. If you're wondering why, read the Containers notes after this.

We can generalize `for` statements like so (from the Containers lecture):
```python
for <name> in <expression>:
    <suite>
```

Here, you evaluate the `<expression>`, which yields something you can iterate over (like a list, which you'll see very shortly, I promise). For each element in this `<expression>`, you bind the element to the `<name>` and then execute the `<suite>`. Once you run out of elements to bind, you exit the loop.

This was a very brief overview of `for` statements. If you're confused, please go on to the Containers notes. All of this will make much more sense after those, which are meant to go hand-in-hand with these.