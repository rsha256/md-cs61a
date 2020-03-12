---
title: "Environments"
date: 2020-02-14T23:34:27-08:00
draft: true
---

If you haven't read my notes on [environment diagrams](../../welcome/env_diags/), now is a good time to read those.

## Parent Frames
With the exception of the global frame, every function's execution frame has a parent: the frame in which the function was created. When you call a function, the function's frame first looks for references within its frame. If it doesn't find one, it goes up a frame and keeps doing this until it hits the global frame. If it still doesn't find a reference to a specified variable or function, the variable or function doesn't exist.

This idea is crucial: a frame can only deal with variables in or above it, and a frame is only created upon execution of a function. This is also why a frame doesn't necessarily become irrelevant upon completion. Check out this [demo](http://pythontutor.com/visualize.html#code=a%20%3D%201%0A%0Adef%20x%28b%29%3A%0A%20%20%20%20c%20%3D%203%0A%20%20%20%20def%20y%28d%29%3A%0A%20%20%20%20%20%20%20%20e%20%3D%205%0A%20%20%20%20%20%20%20%20return%20b%20%2B%20d%20%2B%20e%0A%20%20%20%20return%20y%0A%0Az%20%3D%20x%28a%20%2B%201%29%0Af%20%3D%206%0Az%284%29&cumulative=false&curInstr=0&heapPrimitives=nevernest&mode=display&origin=opt-frontend.js&py=3&rawInputLstJSON=%5B%5D&textReferences=false).

If you step through it, you'll see that the global frame first contains `a` and `x`. When we try to assign `z`, we call `x`, creating a new frame. The first thing that happens is that every parameter gets evaluated and written into the frame. In `x`, we write the value of `b` into the frame right off the bat. Then we add `c` and `y` to our frame. Notice that the function description of `y` contains `[parent=f1]`. This is important -- `f1` is the frame we created for `x`, as it's now labeled. For the context of 61A, you'll always label your frames, even if it becomes irrelevant upon completion. Now, we return `y`, so `x` is done executing. Why doesn't it disappear?

Because there's a reference within the frame of `x` that we could use outside of it. As long as there are references pointing to anything inside that frame, we cannot get rid of it. There is now a `z` value in the global frame, and we proceed to create a new `f` variable. This is mostly to show that `f1` sticks around.

A new frame is created when we call `z` (notice that it's a higher order function).

## What a Frame Entails
Every frame contains variables and functions, and everything in a frame can refer to everything else in that frame.