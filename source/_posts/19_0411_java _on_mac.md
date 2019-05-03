---
layout: post
title: Java On MacOS
date:   2019-04-11 08:24:00
category: [Java]
tags: [Java, MacOS]
---



## About

- JDK: Java development toolkit, the library of Java, using to complie and run Java programs
- J2EE: Java 2 enterprise edition, for enterprise
- J2SE: Java 2 standard edition, standar version
- J2ME: Java 2 Micro Edition, usually for mobile developement

<!--more-->

## Install JDK

If you use Eclipse, you don't have to install Java development, it has one.

### Download JDK

Download JDK from https://www.oracle.com/technetwork/java/javase/downloads/jdk11-downloads-5066655.html

I use `jdk-11.0.2_osx-x64_bin.dmg`

### Installation

After install the dmg file, enter `java -version` in terminal to test whether it is successful:

```
$ java -version
java version "11.0.2" 2019-01-15 LTS
Java(TM) SE Runtime Environment 18.9 (build 11.0.2+9-LTS)
Java HotSpot(TM) 64-Bit Server VM 18.9 (build 11.0.2+9-LTS, mixed mode)
```

## Enviroment

### Add PATH and CALSSPATH

Check the version:

```
$ ls /Library/Java/JavaVirtualMachines/
jdk-11.0.2.jdk
```

Or open Finder, press “Command + Shift + G”, and enter `/Library/Java/JavaVirtualMachines/` to see it.

Edit profile:

```
$ sudo vim /etc/profile
```

Add this at the last:

```
JAVA_HOME="/Library/Java/JavaVirtualMachines/jdk-11.0.2.jdk/Contents/Home/"

CLASS_PATH="$JAVA_HOME/lib"

PATH=".:$PATH:$JAVA_HOME/bin
```

The whole file should be like this:

```
# System-wide .profile for sh(1)

if [ -x /usr/libexec/path_helper ]; then
        eval `/usr/libexec/path_helper -s`
fi

if [ "${BASH-no}" != "no" ]; then
        [ -r /etc/bashrc ] && . /etc/bashrc
fi

JAVA_HOME="/Library/Java/JavaVirtualMachines/jdk-11.0.2.jdk/Contents/Home/"

CLASS_PATH="$JAVA_HOME/lib"

PATH=".:$PATH:$JAVA_HOME/bin"
```

Press `esc` and enter `:wq!` to sava and exit.

Enter this to make it effective:

```
$ source /etc/profile
```

## Test

Write a `Hello.jav` file.

```
class Hello {
     public static void main(String[] args) {
         System.out.println("Hello Laker");
     }
}
```

Compile it :

```
# laker @ Laker in ~/Downloads [21:23:40] C:1
$ javac Hello.java
```

Run it

```
# laker @ Laker in ~/Downloads [21:24:12]
$ java Hello
Hello Laker
```

## Uninstallation

Futhermore, the uninstallation is following command:
https://blog.csdn.net/qq_30889373/article/details/78863313

- Fisrt

```
$ sudo rm -fr /Library/Internet\ Plug-Ins/JavaAppletPlugin.plugin
$ sudo rm -fr /Library/PreferencesPanes/JavaControlPanel.prefpane
```

- Second

Check the version:

```
$ ls /Library/Java/JavaVirtualMachines/
jdk-11.0.2.jdk
```

Remove

```
$ sudo rm -rf /Library/Java/JavaVirtualMachines/jdk-9.0.1.jdk
```


> Exchange blogroll： [http://laker.me/blog]( http://laker.me/blog )
> Github：[https://github.com/younglaker]( https://github.com/younglaker )
