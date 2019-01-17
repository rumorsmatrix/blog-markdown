---
layout: post
title: "Twine: randomly splicing arrays"
tags:
  - programming
  - twine
---

Here's a little Twine thought exercise. Let's say you want to output elements from an array in a random order, with none of them being reused.

First, we set up an array containing our random elements: 

```
(set: $a to (array: "first", "second", "third", "fourth"))
```

Then, we pick a random number to index that array with, and use it to output that array's element -- or do whatever it is we want to do to it. We could use `(goto:)` to send the player to a named passage; thus creating a kind of randomly-generated maze.

```
(set: $r to (random: 1, $a's length))
(print: $a's $r)
```

Point of note: array referencing in Twine2's Harlowe is done with `array's first`, `array's second`, `array's nth`, but you can also just say `array's n`, as above. I wasn't sure if that was going to work, but it does.

Next, we use `(move:)` to move the item from our array into another variable (which we don't care about). This will update the array so that the randomly indexed element is no longer present.

```
(move: $a's $r into $trash)
```

**Note**: As of September 2015, be careful to use *into* and not *to* in the `(move:)` function. Using `to` will set the indexed value to `0`, and not remove it from the array. This is a known bug.

You can test `$a's length` to see how many elements are left, and if the length is zero you know you have dealt with the entire list.
