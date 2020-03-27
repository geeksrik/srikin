---
layout: post
title:  "Starting eclipse with more memory for large projects"
date:   2015-07-13 06:39:49
categories: eclipse, large, projects, java, memory
banner_image: ""
featured: false
comments: true
---

I had come across a situation where my Eclipse IDE used to crash or shutdown forcibly due to less memory being available. After searching around for a while, I came across a command that enables you to start this IDE with more memory. Here it is:

```eclipse -vmargs -Xmx<memory size>```

I have tried combinations of 512M and 1024M (0.5 GB and 1GB respectively) and the IDE worked fine without a crash since then. This is a useful command and I hope you can refer this site for starting up eclipse with more memory in future and avoid some precious time saving IDE crashes in future!

UPDATE: On [this link](http://javahowto.blogspot.com/2006/06/6-common-errors-in-setting-java-heap.html), I also found six common errors one would make while starting up eclipse with virtual memory arguments. I reproduce here the excerpt of the six errors:

Two JVM options are often used to tune JVM heap size: -Xmx for maximum heap size, and -Xms for initial heap size. Here are some common mistakes I have seen when using them:

- Missing m, M, g or G at the end (they are case insensitive). For example,

```java -Xmx128 BigAppjava.lang.OutOfMemoryError: Java heap space```

The correct command should be: java -Xmx128m BigApp. To be precise, -Xmx128 is a valid setting for very small apps, like HelloWorld. But in real life, I guess you really mean -Xmx128m

- Extra space in JVM options, or incorrectly use =. For example,

<pre>
    java -Xmx 128m BigAppInvalid maximum heap size: -XmxCould not create the Java virtual machine.
    java -Xmx=512m HelloWorldInvalid maximum heap size: -Xmx=512mCould not create the Java virtual machine.
</pre>

The correct command should be java -Xmx128m BigApp, with no whitespace nor =. -X options are different than -Dkey=value system properties, where = is used.

- Only setting -Xms JVM option and its value is greater than the default maximum heap size, which is 64m. The default minimum heap size seems to be 0. For example,

```
java -Xms128m BigAppError occurred during initialization of VMIncompatible initial and maximum heap sizes specified
```

The correct command should be java -Xms128m -Xmx128m BigApp. It’s a good idea to set the minimum and maximum heap size to the same value. In any case, don’t let the minimum heap size exceed the maximum heap size.

- Heap size is larger than your computer’s physical memory. For example,

```
java -Xmx2g BigAppError occurred during initialization of VMCould not reserve enough space for object heapCould not create the Java virtual machine.
```

The fix is to make it lower than the physical memory: java -Xmx1g BigApp

- Incorrectly use mb as the unit, where m or M should be used instead.

```
java -Xms256mb -Xmx256mb BigAppInvalid initial heap size: -Xms256mbCould not create the Java virtual machine.
```

The heap size is larger than JVM thinks you would ever need. For example,
java -Xmx256g BigAppInvalid maximum heap size: -Xmx256gThe specified size exceeds the maximum representable size.Could not create the Java virtual machine.
The fix is to lower it to a reasonable value: java -Xmx256m BigApp

- The value is not expressed in whole number. For example,

```
java -Xmx0.9g BigAppInvalid maximum heap size: -Xmx0.9gCould not create the Java virtual machine.
```

The correct command should be java -Xmx928m BigApp