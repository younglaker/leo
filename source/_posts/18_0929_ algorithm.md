---
layout: post
title:  算法学习1：重新排序链表
date:   2018-09-29 08:24:00
category: [算法]
tags: [算法]
---

<!-- ![算法学习：重新排序链表][1] -->



## 题目
给定一个单链表，将链表按头节点、尾节点、第二个节点、 倒数第二个节点...的规律重建。要求：原地操作，不改变节点的值。

<!--more-->

## 思路
暴力法：先找头节点，再找尾节点，然后顺次第二个节点，倒数第二个节点，由于是单链表，不停的从表头遍历到表尾，时间复杂度O(n^2)

看下有没有其他便捷方法。

假设给一组数字`1,2,3,4,5,6`，重新排序后是`1,6,2,5,3,4`，会发现一个规律，`1, 2, 3`是顺序的，`6, 5, 4`是倒序插入的。

所以可这样考虑：
先把链表一分为二，把后半部分数据倒序插入前半部分。
头插法制作倒序链表，时间复杂度 O(n)，将左右两链表合并，时间复杂度 O(n)。总时间复杂度为O(n)。

## 伪代码
```
void Revert (Link L1) {
	new Link L2; //用于存放倒序的后半部链表
	int half_len = L1.lenght() / 2; //记录链表的一半
	int *p = L1->head; //p 指向 L1 头节点
	int *q = L2->head; //q 指向 L2 头指针
	int *s, *t;

	for (int i = 0; i < half_len; i++) {
		s = s->next; // 找到链表中部
	}

	q = s->next; //把后半段链表赋值给 L2
	s->next = null; // 此时 s 为 L1尾指针

	t = q->next;
	// 这里我直接在表内操作，看起来有点乱，新建个 L3来存放会看得舒服点
	while ( t->next != null ) { //倒置 L2
		q->next = t->next;
		t->next = q;
		L2->head->next = t;
		t = q->next;
		q = L2->head->next;
	}

	while ( p != s ) { // p 没有走到表尾时插入L2节点
		t = L2->head->next; //一开始，t 指向 L2第一个节点
		L2->head->next = L2->head->next->next; //取出第一个节点，第二个节点变成第一个节点
		t->next = p->next; //t 插入 p
		p->next = t->next;
		p = p->next->next; //移动 p 到下一个待插入的节点
	}

}
```

简单的图示：

![图示][2]

> 欢迎交换友链： [laker.me--进击的程序媛]( http://laker.me/blog )
> Github：[https://github.com/younglaker]( https://github.com/younglaker )
> V信: lakerHQ （请注明‘来自博客’）

  [1]: http://wx2.sinaimg.cn/large/6d184cefly1fvwi0uvwsmj20p0046gm8.jpg
  [2]: https://raw.githubusercontent.com/aomine-sama/px/master/2018/18092901.jpg
