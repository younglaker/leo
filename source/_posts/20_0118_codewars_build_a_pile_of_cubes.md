---
layout: post
title: Algorithm - Build a pile of Cubes
date: 2020-01-18 08:24:00
category: [Algorithm]
tags: [Algorithm, CodeWars]
---

## Description

https://www.codewars.com/kata/5592e3bd57b64d00f3000047/train/javascript

The parameter of the function findNb (find_nb, find-nb, findNb) will be an integer m and you have to return the integer n such as n^3 + (n-1)^3 + ... + 1^3 = m if such a n exists or -1 if there is no such n.

<!--more-->

Example :

```
findNb(1071225) --> 45
findNb(91716553919377) --> -1
```

## Solution:

https://github.com/younglaker/codewars

## Approach


### Approach one

To find whether there is a sum equals to m.

```
function findNb(m) {
    let sum = 0
    for (var i = 1; sum < m; i++) {
    	sum += i ** 3
    }
    return sum === m ? i - 1 : -1
}
```

Shorten the code, count the sum in for():

```
function findNb(m) {
    for(var i = 1, sum = 0; sum < m; sum +=i ** 3, i++);
    return sum == m ? (i-1) : -1;
}
```
### Approach two

`return m ? -1 : n`:

- m < 0 => true => -1
- m > 0  => false => n

```
function findNb(m) {
  var n = 0
  while (m > 0) m -= ++n ** 3
  return m ? -1 : n
}
```

.
> Exchange blogroll： [http://laker.me/blog]( http://laker.me/blog )
> Github：[https://github.com/younglaker]( https://github.com/younglaker )
