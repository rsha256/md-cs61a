---
title: "Macros"
weight: 1
---

So far, we've seen some of the basics of Scheme that are parallel to the concepts we learned with Python. Things like procedures, recursion, etc., are pretty standard across most programming languages. One of the things that not a lot of languages offer, though, is macros.

## Motivation

Consider this: you're reading some text on a screen, and you want to select all of it and copy it. You could drag your cursor from the start of the text to the end, right click, and hit "Copy," or you could just press Ctrl+A, Ctrl+C. The keyboard shortcut does the same thing as the first process. In fact, you can imagine that the keyboard shortcut actually *performs* the first process under the hood.

This is precisely the motivation behind macros -- say you're writing some code to be evaluated twice. In Scheme, you could achieve this as follows:

```scheme
(begin (print 'woof) (print 'woof))
```

This code will print the word `woof` to the console twice, as desired. However, say now that you wanted to replace this code with a much larger process:

```scheme
(define x 5)
(begin
    (if (= x 2) 5 x)
    (if (= x 2) 5 x)
)
```

I wrote the first `if` procedure and copy-pasted it. Then, I realized that there's a typo -- I meant to check if `x` is `5`, not `2`. Now, I need to go back and change two lines of code. Notice also that we're repeating ourselves here -- our first rule in CS 61A is DRY: Don't Repeat Yourself.

There *has* to be a way for us to make a procedure do this repetition for us, right?

```scheme
(define (twice f)
    (begin f f)
)

(twice (print 'woof))
```

Does this work? Not quite. Remember the rules of evaluation for non-special forms: you get the procedure, you evaluate the operands, you apply the procedure to the evaluated operands. This means that `(print 'woof)` is evaluated before you even call `twice`, which actually just takes in two `undefined`s. How do we make Scheme take in a raw command without evaluating it? Macros!

Think about this. Every command is just a chain of characters, right? "(print 'woof)" is just a string that *happens* to be a valid Scheme expression. So why can't we just pass it in as a raw string and tell Scheme to construct a new raw string out of it that can be evaluated? Well, we can!

## Circumventing Rules of Evaluation

```scheme
(define-macro (twice f)
    `(begin ,f ,f)
)

(twice (print 'woof))
```

Let's walk through this example. The way a macro works is that Scheme actually doesn't evaluate the operands -- it treats them as regular strings. What our macro does is it uses a template to construct a new string that Scheme can evaluate. Here's what's going on:

1. We call the `twice` macro with the string `"(print 'woof)"`.
2. The `twice` macro has a quoted template (see the quasiquoting review below) that creates the string `"(begin <f> <f>)"` where `<f>` is replaced with the string we passed in.
3. The `twice` macro returns the unevaluated string `"(begin (print 'woof) (print 'woof))"`, which Scheme subsequently evaluates in the same frame from where we called `twice`.

**The way that macros are evaluated in Scheme can be summarized in the following 3 steps:**
1. Evaluate the operator to check if a macro of that name exists.
2. Evaluate the body of the macro procedure using *unevaluated* operands. The macro should *not* return a result, rather an expression that can be evaluated as Scheme code.
3. Evaluate the expression returned by the macro. Usually, this is the first time any of your operands actually get evaluated. This evaluation occurs in the same frame as where you called the macro -- *not* inside a new frame for the macro.

## Quasiquoting Review
Recall that quoting and quasiquoting are both ways to create strings/lists in Scheme. The difference is that a quoted list is completely raw, while a *quasi*quoted list is essentially a template: everything that's unquoted in a quasiquoted list is an element in the template that can be replaced.

```scheme
'(x 2 3)  ; this is the equivalent of ['x', 2, 3] in Python
`(x 2 3)  ; this is the equivalent of ['x', 2, 3] in Python
`(,x 2 3) ; this is the equivalent of [x, 2, 3] in Python (note the lack of quotes around `x`)
```

For our `twice` macro, then, you can imagine our template to be something like this in Python:

```python
>>> f = "(print 'woof)"
>>> print_woof_twice = "(begin " + f + " " + f + ")"
>>> print_woof_twice
"(begin (print 'woof) (print 'woof))"
```

And then we evaluate this as a Scheme expression, because we assume that it's a valid one :)

## Example: The `or` Macro
You may recognize this example from discussion, but we'll look at it anyway. Say we want to create a macro that performs the same way as the `or` special form, but only for two expressions because variadics are messy.

Without using a macro, the way we would replicate the `or` form would likely be using the `if` form: the first operand will always be evaluated, and if it's truthy, we'll return the second operand. If not, then we return the third operand. To make this replicate `or`, the first and second operand will just be our first expression, and the third will be our second expression (only evaluated if the first one is false).

```scheme
(if (print 'bork) (print 'bork) (/ 1 0))
```

This will print `bork` twice, as `print` returns `undefined` which is a truthy value in Scheme. Naturally, we'd probably only want to evaluate the expression once, and since we *know* it'll be evaluated no matter what (it's our condition!), we can wrap our `if` in a `let` form and set the result of evaluating `print` to a variable.

```scheme
(let ((v1 (print 'bork)))
    (if v1 v1 (/ 1 0))
)
```

We evaluate `print` once, and set `v1` to `undefined`. Then, our `if` form simplifies to `(if undefined undefined (/1 0))`. No double evaluation of `print`! How do we make this code a bit more reusable? Well, `(print 'bork)` is essentially a placeholder for any first expression, and `(/ 1 0)` for any second expression. Let's see if we can write a macro that accounts for this:

```scheme
(define-macro (or-macro expr1 expr2)
    `(if ,expr1 ,expr1 ,expr2)
)

(or-macro (print 'bork) (/ 1 0))
```

This is parallel to our first attempt, where `print` gets evaluated twice. Now, here's the tricky part: how do we wrap this in `let`?

```scheme
(define-macro (or-macro expr1 expr2)
    `(let ((v1 ,expr1))
        (if v1 v1 ,expr2)
    )
)

(or-macro (print 'bork) (/ 1 0))
```

**Notice that we don't unquote `v1`!** This is because our returned Scheme expression actually defines `v1` within itself; unquoting is used to refer to variables that are defined outside of the string we're working with. In this case though, `v1` does *not* exist outside of the quote. It is defined inside our template, so we don't need to replace it with anything -- we want to keep the variable `v1` in our final expression before it's evaluated!

## Note About Complexity
Macros are arguably one of the hardest concepts taught in 61A. To be very honest, I didn't understand them when I took this class. It took me another semester and a half to finally figure out how macros work and why they're so useful, so if you don't get them right off the bat, that's perfectly fine. Don't stress about it -- just read over as many resources as you can, get different explanations about them. The more explanations you hear, the more you'll understand what macros are. And if all else fails, try teaching them! In general teaching something you don't understand is a great way to figure out *why* you don't understand it -- this is actually how I learned macros! I talked through them with a rubber duck and realized exactly which parts confused me. From there, it was just a matter of figuring out the answers to those particular questions :)
