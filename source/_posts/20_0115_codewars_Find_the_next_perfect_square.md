---
layout: post
title: Algorithm - Find the next perfect square
date: 2020-01-15 08:24:00
category: [Algorithm]
tags: [Algorithm, CodeWars]
---

## Description

https://www.codewars.com/kata/56269eb78ad2e4ced1000013/javascript

Complete the findNextSquare method that finds the next integral perfect square after the one passed as a parameter. Recall that an integral perfect square is an integer n such that sqrt(n) is also an integer.

If the parameter is itself not a perfect square, than -1 should be returned. You may assume the parameter is positive.

<!--more-->

Example :

```
indNextSquare(121) --> sqrt(121)=11 is integer, (11+1)*(11+1)=144 returns 144
findNextSquare(625) --> returns 676
findNextSquare(114) --> returns -1 since 114 is not a perfect
```

## Solution:

https://github.com/younglaker/codewars

### Approach

The main part is to check whether the Math.sqrt(sq) is integer.

### Using regular expression:

```
function findNextSquare(sq) {
  // Return the next square if sq if a perfect square, -1 otherwise
  let number = Math.sqrt(sq)

  return /^[\d]+$/.test(number.toString()) ? (number + 1) ** 2 : -1;
}

```

### remainder

Math.sqrt(121)%1 = 0 = false
Math.sqrt(122)%1 = 0.045361017187261155 = true

```
function findNextSquare(sq) {
  return Math.sqrt(sq)%1? -1 : Math.pow(Math.sqrt(sq)+1,2);
}

```

### Math.round, Math.ceil, Math.floor

Math.round(1) === 1
Math.round(1.1) = 1 != 1.1

```
Math.round(number) === number)
```

### Number.isInteger


```
Number.isInteger(sqrt)
```


### parseInt

```
if(parseInt(number) === number)
```

### Bit operation


```
if(parseInt(number | 0) === number)
```

.
> Exchange blogroll： [http://laker.me/blog]( http://laker.me/blog )
> Github：[https://github.com/younglaker]( https://github.com/younglaker )
