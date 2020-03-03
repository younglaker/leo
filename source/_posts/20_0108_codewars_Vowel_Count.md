---
layout: post
title: Algorithm - Vowel Count
date: 2020-01-08 08:24:00
category: [Algorithm]
tags: [Algorithm, CodeWars]
---

## Description

https://www.codewars.com/kata/54ff3102c1bad923760001f3/javascript

Return the number (count) of vowels in the given string.

We will consider a, e, i, o, and u as vowels for this Kata.

The input string will only consist of lower case letters and/or spaces.

<!--more-->

Example :

```
 Test.assertEquals(getCount("abracadabra"), 5)
```

## Solution:

https://github.com/younglaker/codewars

### Approach 1
Split the sting into a array, the check each letter:

```
function getCount(str) {
  var vowelsCount = 0;

  let arr = str.split('');
  for (let i = 0; i < arr.length; i++){
    if (arr[i] === 'a' || arr[i] === 'e' || arr[i] === 'i' || arr[i] === 'o' || arr[i] === 'u') {
      vowelsCount+=1;
    }
  }

  return vowelsCount;
}
```

### Approach 2
`x.match(/[sabticl]/ig` to select all matched letters into a array. `|| []` is order to avoid error when there is no matched letter for `.length`.


```
function getCount(str) {
  return (str.match(/[aeiou]/ig) || []).length
}
```

### Approach 3

Delete the letter dosen't match, then count the length:

```
function getCount(str) {
  return str.replace(/[^aeiou]/gi, '').length;
}
```

.
> Exchange blogroll： [http://laker.me/blog]( http://laker.me/blog )
> Github：[https://github.com/younglaker]( https://github.com/younglaker )
