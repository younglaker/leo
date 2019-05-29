---
layout: post
title: Homebrew updating problem
date:   2019-05-03 08:24:00
category: [Mac]
tags: [Java, MacOS]
---


There are two common problem when updating brew.

<!--more-->

## Permission denied
> brew update Homebrew/.git/FETCH_HEAD: Permission denied

When you run `brew doctor`, you can find there some permission problem with the `/usr/local/` files.

![image](https://raw.githubusercontent.com/aomine-sama/px/master/common/19050301.jpg)

You should change the permission, run this:

    sudo chown -R YOURNAME:admin /usr/local


## Could not read Username

> brew update fatal: could not read Username for 'https://github.com': terminal prompts disabled

```
# laker @ Laker in ~ [11:03:59] C:1
$ brew update
git: 'credential-osxkeychain' is not a git command. See 'git --help'.git: 'credential-osxkeychain' is not a git command. See 'git --help'.

fatal: could not read Username for 'https://github.com': terminal prompts disabled
fatal: could not read Username for 'https://github.com': terminal prompts disabled
Error: homebrew/homebrew-x11 does not exist! Run 'brew untap homebrew/homebrew-x11'
homebrew/homebrew-dupes does not exist! Run 'brew untap homebrew/homebrew-dupes'
```


Run the command it recommend:

```
# laker @ Laker in ~ [11:05:57] C:1
$ brew untap homebrew/homebrew-x11
Untapping homebrew/x11...
Untapped (242 files, 224.9KB).

# laker @ Laker in ~ [11:06:39]
$ brew untap homebrew/homebrew-dupes
Untapping homebrew/dupes...
Untapped 36 formulae (277 files, 263.5KB).
```

Then we can update sucessfully:

```
# laker @ Laker in ~ [11:06:44]
$ brew update
Already up-to-date.
```