---
layout: post
title:  "Fred’s C++ Notes: A Must Read Sequence Of Good C++ Examples"
date:   2015-07-08 05:47:49
categories: fred, c++, notes, tutorials
banner_image: ""
featured: false
comments: true
---

I was going through Fred’s C++ site for an example of string streams. This was for a basic requirement of putting in any value into a string, such as a float or an integer, or even more complex values.


    #include <iostream>
    #include <sstream>
    using namespace std;
    . . .
    ostringstream outs;  // Declare an output string stream.
    . . .
    outs << sqrt(2.0);   // Convert value into a string.
    s = outs.str();  // Get the created string from the output stream.

This example was so simple, yet conveyed the point. The square root of 2.0 was stored into a string stream designated as outs. One could then always get back the string value from ‘outs’ as and when required. If the ostringstream class were not to be there, you can only imagine what pain one has to go through using itoa or its equivalents such as the sprintf command, etc to get the same job done!

For those who would like to know more about these examples, please do read through this CHM help file which has a compilation of all Fred’s works until now (with his prior permission)

>Hi Srikanth,

>I don’t have any PowerPoint slides — sorry. You are free to use my online notes in any way you want. I’m glad you find them useful.

>Yours, Fred. 

Do [click here](https://www.dropbox.com/s/lvljgysfvwjlcd3/fred_c%2B%2B.chm) to get access to Fred’s programming tricks and techniques. You won’t leave the site unhappy I promise!

Technorati : C++, Fred, anything to string, chm, class, help file, integer to string, ostringstream, string stream