---
layout: post
title:  "10 things to remember while writing/porting (portable) C code"
date:   2015-07-08 06:08:49
categories: Software Development, Software Development, Portable C code, Porting Guidlines, Checklist for porting c code, Embedded C programming, Alignment, Byte ordering
banner_image: ""
featured: false
comments: true
---

Embedded Programmers spend a large amount of time porting existing code from one platform to another; compile it on various compilers based on platform needs. I have tried to make a check list which would address this concern. Am pretty convinced the list is not complete, but covers majority of the issues to be take care of-

1>Difference in word size

Eg: ‘int’ is not always 4 bytes. It can be 2 bytes, 4 bytes etc.

NOTE: We can assume ‘int’ to be of native size. Eg: On 32 machine ‘int’ is always 4 bytes and on 64 bit machine it is 8 bytes!!

2>Problems in Byte Ordering

Most of the embedded guys are aware of little and big endian issue.

3> Alignment issues

This is also a well known issue and most of the programmers almost relateto ‘padding’ keyword. Some systems can load/store from even address only and few others only from odd address. We can also classify this into byte aligned, word aligned systems.

4> Function Argument syntax

Functions parameters are pushed on to stack left to right on some systems and vice versa on few others.

5> Using pointers

Beware when you are trying to use function pointers and data pointers interchangeably. The behavior might be different across compilers.

6> Floating Point Accuracy

The range, precision, accuracy of floating point representation varies from compiler to compiler.

7> Evaluation order

This is also well known issue. Specifically programmers have seen different results when they run their programs on different compilers with expressions involving ++,– etc.

8> Optimization dependent

If a section of a code is heavily dependent on the specific optimization ( memory/code) providing by a compiler, programmer will have tough time in porting it onto other compiler which doesn’t support that optimization.

9> Bit Fields, structures and unions

Above mentioned issues – word size, byte order and alignment all of them have major impact on these data structures.

10> Machine specific arithmetic

Few arithmetic operators like ‘shift’ and ‘division-/’ have machine dependencies if operands are negative. (I am yet to see this practically happening!!)

Can you add few more to this list??

Technorati Tags: Software Development, Software Development, Portable C code, Porting Guidlines, Checklist for porting c code, Embedded C programming, Alignment, Byte ordering.