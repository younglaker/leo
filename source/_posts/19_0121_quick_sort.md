---
layout: post
title: Algorithm - Quick Sort by Python
date:   2019-01-22 08:24:00
category: [Algorithm]
tags: [Algorithm,Python]
---

![Django Enviroment in Tencent Cloud Ubuntu](http://wx2.sinaimg.cn/large/6d184cefly1fvwi0uvwsmj20p0046gm8.jpg)

<!--more-->

> Exchange blogroll： [http://laker.me/blog]( http://laker.me/blog )
> Github：[https://github.com/younglaker]( https://github.com/younglaker )

There are tow method to set pivot.The easy way is setting the first item as pivot, and the other way is setting the middle item as pivot.

The first way is more easy to understand and write code.
The second way is a little better than the first one when the list is mostly ordered, it can seperate the smaller and bigger items to two sides, but in first way , one side may has all items and the other side has no item.

## Method one

Set the first item as pivot.

```
def quick_sort(list, start, end):
    # If start smaller than end, continue sorting
    if start < end:
        left = start
        right = end

        # Set the first item as pivot
        pivot = list[left]

        # Do compare while pointer left smaller than right
        # Move the smaller one to left part and bigger one to right part
        while left < right:
            #if the item of  pointer right item bigger than move the pointer right back
            while (left < right) and (list[right] >= pivot):
                right -= 1

            # Now, we find the a item smaller than pivot,so set list[left] = list[right]
            if left < right:
                list[left] = list[right]
                left += 1

            # Than we scan left part in than same way
            while (left < right) and (list[left] <= pivot):
                left += 1

            # Now, we find the a item bigger than pivot,so set list[right] = list[left]
            if left < right:
                list[right] = list[left]
                right -= 1


        # After comparison, the list is separated to two parts,
        # and pointer left and right are in the same place
        # So we set pivot in this place
        list[left] = pivot
        print(list)

        #递归前后半区
        # Now recurse the quick_sort(）
        # Left part is [start, left - 1]
        # Right part is [right + 1, end]
        quick_sort(list, start, left - 1)
        quick_sort(list, right + 1, end)
    return list

if __name__ == "__main__":

    before = [5, 3, 4, 6, 12, 2, 8]

    print("Result:")
    after = quick_sort(before, 0, len(before)-1 )
    print(after)
```

Take a example:

![example](https://ws3.sinaimg.cn/mw690/6d184cefly1fyfxtd5g6lj21jg25cnmx.jpg)


## Method two

Set the middle item as pivot.

```
def quickSort(list, start, end):

    if start >= end:
        return False

    # Set new pointers
    left, right = start, end

    mid = (start + end) // 2

    # Exchange pivot and the last item,
    # in order to make the last one not to be overwrite by next step
    # As the we have a new parameter 'pivot', so we don't be afaid of being overwrite
    # Actually, it can be any other value
    pivot = list[mid]
    list[mid] = list[end]
    list[end] = pivot

    # The following code is the similar to method one
    # But pay attention, here we start from left part,
    # Because we set the useless value to the last item,
    # which will be overwrite by a lager number from left part
    while left != right:
        while left < right and list[left] <= pivot:
            left += 1

        if left < right:
            list[right] = list[left]
            right -= 1

        while left < right and list[right] >= pivot:
            right -= 1

        if left < right:
            list[left] = list[right]
            left += 1

    list[right] = pivot

    quickSort(list, start, right-1)
    quickSort(list, right+1, end)
    return list

a = [5, 3, 10, 6, 12, 2, 8]
a = quickSort(a, 0, len(a)-1)
print(a)
```

Take a example:

![example](https://wx3.sinaimg.cn/mw690/6d184cefly1fyfxj2g1pdj21lg27ye81.jpg)