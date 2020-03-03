---
layout: post
title: Algorithm - The Office VI Sabbatical
date: 2020-01-10 08:24:00
category: [Algorithm]
tags: [Algorithm, CodeWars]
---

## Description

https://www.codewars.com/kata/57fe50d000d05166720000b1/train/javascript

val=your value to the organisation
happ=her happiness level at the time of asking and finally
The numbers of letters from 'sabbatical' that are present in string 'x'.

If the sum of the three parameters (as described above) is > 22, return 'Sabbatical! Boom!', else return 'Back to your desk, boy.'. memory?

<!--more-->

Example :

```
Test.assertEquals(sabb('Can I have a sabbatical?', 5, 5), 'Sabbatical! Boom!');
Test.assertEquals(sabb('Why are you shouting?', 7, 2), 'Back to your desk, boy.');
Test.assertEquals(sabb('What do you mean I cant learn to code??', 8, 9), 'Sabbatical! Boom!');
Test.assertEquals(sabb('Please calm down', 9, 1), 'Back to your desk, boy.');
```

## Solution:

https://github.com/younglaker/codewars

## Approach

```
function sabb(x, val, happ){
  let sum = (x.match(/[sabticl]/ig )|| []).length;

  if(sum + val + happ > 22) {
    return 'Sabbatical! Boom!'
  } else {
    return 'Back to your desk, boy.'
  }

}
```

`x.match(/[sabticl]/ig` to select all matched letters into a array. `|| []` is order to avoid error when there is no matched letter for `.length`.

Shorten the code to below:

```
function sabb(x, val, happ){

  return (x.match(/[sabticl]/ig )|| []).length + val + happ > 22 ? 'Sabbatical! Boom!' : 'Back to your desk, boy.'


```

.
> Exchange blogroll： [http://laker.me/blog]( http://laker.me/blog )
> Github：[https://github.com/younglaker]( https://github.com/younglaker )
