---
layout: post
title: Algorithm - Find the divisors
date: 2020-01-20 08:24:00
category: [Algorithm]
tags: [Algorithm, CodeWars]
---

## Description

https://www.codewars.com/kata/544aed4c4a30184e960010f4/train/javascript

Create a function named divisors/Divisors that takes an integer n > 1 and returns an array with all of the integer's divisors(except for 1 and the number itself), from smallest to largest. If the number is prime return the string '(integer) is prime'

<!--more-->

Example :

```
divisors(12); // should return [2,3,4,6]
divisors(25); // should return [5]
divisors(13); // should return "13 is prime"
```

## Solution:

https://github.com/younglaker/codewars

## Approach


### i <= integer / 2



```
function divisors(integer) {
  let arr = []
  for (var i = 2; i <= integer / 2; i++) {
    if (integer / i % 1 === 0)
      arr.push(i)
  }

  return arr.length ? arr : integer +" is prime"
};
```

### i < Math.sqrt(integer)


```
function divisors(integer) {
  let arr = []
  for (var i = 2; i < Math.sqrt(integer); i++) {
    if (integer / i % 1 === 0)
      arr.push(i, integer / i)
  }

  return arr.length ? arr.sort(sortNumber) : integer +" is prime"
};

function sortNumber(a, b){ // Ascending order
    return a - b
}
```

> sort() will change the number into string to sort

```
[12, 2, 3, 4, 6, 8,1,110].sort()

```

get:

```
[1, 110, 12, 2, 3, 4, 6, 8]

0: 1
1: 110
2: 12
3: 2
4: 3
5: 4
6: 6
7: 8
```


.
> Exchange blogroll： [http://laker.me/blog]( http://laker.me/blog )
> Github：[https://github.com/younglaker]( https://github.com/younglaker )
