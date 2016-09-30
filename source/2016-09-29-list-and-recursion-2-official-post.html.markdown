---
title: list-and-recursion-2-official-post
date: 2016-09-29 20:18 UTC
tags: Elixir
---

# __**Elixir**__

## List and Recursions

I'm currently reading the Programming Elixir book by Dave Thomas, which has been
very good so far! Slowly but surely, I'm picking up some Elixir skills. I maybe should start
from the beginning sometime soon, but now that I'm starting to blog in the middle of the book, I'll
just start with the current problem, and try to fill in any weird Elixir tricks.

_Exercise: ListAndRecursion-2_

>Write a `max(list)` that returns the element with the maximum value in the list (This
is slightly trickier than it sounds.)

So the solution is what I came up to get it to work. I will talk about some mistakes that I made along the way
and fix up the final solution.

Here is my solution:

``` elixir
def choose(a, _, true), do: a
def choose(_, b, false), do: b

def findMaxNumber([], value), do: value
def findMaxNumber([head|tail]), do: findMaxNumber(tail, head)
def findMaxNumber([head|tail], value ) do
    findMaxNumber(tail, choose(head, value, head>value))
end
```

Let me try to explain.

When using `findMaxNumber(list)` with the `list = [0,1,5,2]`, we call the first function.

```
iex(1)> findMaxNumber(list)
```

Which then matches

``` elixir
def findMaxNumber([head|tail]), do: findMaxNumber(tail, head)
```

In Elixir, and many other languages, a List is simply two nodes, where `head` is the first item in the list, while the tail is the rest of the items.

So when an array of `[1,2,3,4,5]` is broken down, `head = 1` while `tail = [2,3,4,5]`

``` elixir
def findMaxNumber(tail, head)
```

ends up calling

``` elixir
def findMaxNumber([head|tail], value)
```

which looks like the following:

``` elixir
def findMaxNumber([1|[5,2]], 0)
```

and calls `findMaxNumber` recursively while passing in the function `choose`. `choose` would return the greater value of the two
values. It looks like this:

`findMaxNumber([5,2], choose(1, 0, 1>0))`

since `1>0`, the choose function `def choose(a, _, true), do: a` will match, since it's true.

then calls `findMaxNumber` again with the new variables:

`findMaxNumber([5|[2]], 1)`

This time, `head` will be greater than `value`! so the recursive function

`findMaxNumber([2], choose(5, 1, 5>1))` would make `choose` return true.

the next iteration would look like this: <br/>
`def findMaxNumber([2|[]], 5), do:` <br/>
`findMaxNumber([], choose(2, 5, 2>5))`<br/>

`choose(2, 5, 2>5))` would match the false choose function which is `def choose(_, b, false), do: b`
and 5 would remain the higher value.

Since the last function will be `findMaxNumber([], value)`, it would just return the value!

That's the solution. There's an  issue I need to get to.

## Refactor Time

First, I noticed I can refactor the `choose` functions.

``` elixir
def choose(a, _, true), do: a
def choose(_, b, false), do: b
```
can be

``` elixir
def choose(a, b) when a > b, do: a
def choose(a, b) when a <= b, do: b
```

I've been able to refactor the function this far...

``` elixir
def choose(a, b) when a > b, do: a
def choose(a, b) when a <= b, do: b

def findMaxNumber([head | tail]), do: findMaxNumber(tail, head)
def findMaxNumber([head|tail], value ) do
    findMaxNumber(tail, choose(head, value))
end

def findMaxNumber([], value), do: value
```

Definitely fun stuff!