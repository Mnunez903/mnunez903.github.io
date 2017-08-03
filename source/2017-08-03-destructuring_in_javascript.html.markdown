---
title: Destructuring Objects in Javascript
date: 2017-08-03 19:21 UTC
tags: Javascript
---

Hey! I've been doing some good ol es6/babel related Javascript, and destructuring has been something I seem to always
forget! This entry will simply be a refresher for me (and hopefully, for you too) on how to destructure javascript objects!

Let's start with some object I'm going to use for the rest of this example:

```javascript
const human = {
  name: 'bobby',
  head: {
    eyes: 'brown',
    ears: 'normal',
    mouth: {
      color: 'red',
      voice: 'loud'
    }
  },
  height_in_inches: '70',
  two_thumbs: true
}
```

## Destructuring regular variables

Boom. You want to be able to grab data from an object. Rather than:

```javascript
const eyes = human.head.eyes;
```

You can destructure the variable by doing the following:

```javascript
const { eyes } = human.head;
```

Pretty neat, considering you don't have to type `eyes` twice when you want the variable name to be the same. SWEET!!

## Renaming a constant variable while destructuring

Let's suppose you want to rename a value without changing the results from an API. Note that this API uses snake case
rather than camel case. You would have to do the following:

```javascript
const heightInInches = human.height_in_inches;
```

With destructuring javascript, renaming a variable is a breeze! Here's how to do it:

```javascript
const { height_in_inches: heightInInches } = human;
```

`heightInInches` will be the name of variable.

## Extracting nested data within an object

What if you need to extract multiple variables from nested data? for example, you might want the human's `head`, as well as the `eyes` and `ears` from within the `head`. Naively, you might try a two step approach, first getting the `head` from the `human`, and then the data within it:

```javascript
const { name, head } = human;
const { eyes, ears } = head;
```

But wait! You can do that all in one shot! Here's how:

```javascript
const {
    name,
    head,
    head: { eyes, ears }
} = human;
```

When you console.log:

```javascript
console.log(name); //=> bobby
console.log(head); //=> { eyes: 'brown', ears: 'normal', mouth: { color: 'red', voice: 'loud'} }
console.log(eyes); //=> brown
console.log(ears); //=> normal
```

Now, you've learned how to destructure, rename while destructuring, and extracting nested data within an object!

![Go be Destruct-(Wo)Man!](https://media.giphy.com/media/l3vR6jBTvJyYrr3Uc/giphy.gif)
