---
layout: post
title:  "The Year 2038 Time Problem"
date:   2015-07-10 06:09:49
categories: Software Development, 2038, Y2k, Y3k, Computers, Programming, Time problem, Dates, IT industry, Bangalore, Bengaluru, Blog, Technology, Unix, Linux, Windows, Pc
banner_image: ""
featured: false
comments: true
---

So we all thought only Y2k and Y3k could cause problems in the world of computing? What about Y2.038k ?? Whats great about this date? Lets have a look. The rest of this article is as quoted by Roger M. Wilcox.

#What’s So Special About 2038?

Early UNIX programmers had quite a sense of humor. In their documentation for the tunefs utility, a command-line program that fine-tuned the file system on the machine’s hard disk, a note at the end reads "You can tune a file system, but you can’t tune a fish." A later generation of UNIX authors, fearful that stuffy, humorless corporate drones would remove this cherished pun, added a programmer’s comment inside the documentation’s source code that read, "Take this out and a UNIX demon will dog your steps until the time_t’s wrap around!"

On January 19, 2038, that is precisely what’s going to happen.

For the uninitiated, time_t is a data type used by C and C++ programs to represent dates and times internally. (You Windows programmers out there might also recognize it as the basis for the CTime and CTimeSpan classes in MFC.) time_t is actually just an integer, a whole number, that counts the number of seconds since January 1, 1970 at 12:00 AM Greenwich Mean Time. A time_t value of 0 would be 12:00:00 AM (exactly midnight) 1-Jan-1970, a time_t value of 1 would be 12:00:01 AM (one second after midnight) 1-Jan-1970, etc.. Since one year lasts for a little over 31 000 000 seconds, the time_t representation of January 1, 1971 is about 31 000 000, the time_t representation for January 1, 1972 is about 62 000 000, et cetera.

If you’re confused, here are some example times and their exact time_t representations:

    | Date & time					| time_t representation	|
    | :----------------------------	| --------------------: |
    | 1-Jan-1970, 12:00:00 AM GMT 	| 0 					|
    | 1-Jan-1970, 12:00:01 AM GMT	| 1 					|
    | 1-Jan-1970, 12:01:00 AM GMT	| 60 					|
    | 1-Jan-1970, 01:00:00 AM GMT	| 3 600 				|
    | 2-Jan-1970, 12:00:00 AM GMT	| 86 400 				|
    | 3-Jan-1970, 12:00:00 AM GMT	| 172 800 				|
    | 1-Feb-1970, 12:00:00 AM GMT	| 2 678 400 			|
    | 1-Mar-1970, 12:00:00 AM GMT	| 5 097 600 			|
    | 1-Jan-1971, 12:00:00 AM GMT	| 31 536 000 			|
    | 1-Jan-1972, 12:00:00 AM GMT	| 63 072 000 			|
    | 1-Jan-2003, 12:00:00 AM GMT	| 1 041 379 200 		|
    | 1-Jan-2038, 12:00:00 AM GMT	| 2 145 916 800 		|
    | 19-Jan-2038, 03:14:07 AM GMT	| 2 147 483 647 		|
    
    
By the year 2038, the time_t representation for the current time will be over 2 140 000 000. And that’s the problem. A modern 32-bit computer stores a "signed integer" data type, such as time_t, in 32 bits. The first of these bits is used for the positive/negative sign of the integer, while the remaining 31 bits are used to store the number itself. The highest number these 31 data bits can store works out to exactly 2 147 483 647. A time_t value of this exact number, 2 147 483 647, represents January 19, 2038, at 7 seconds past 3:14 AM Greenwich Mean Time. So, at 3:14:07 AM GMT on that fateful day, every time_t used in a 32-bit C or C++ program will reach its upper limit.

One second later, on 19-January-2038 at 3:14:08 AM GMT, disaster strikes.


To know more about this problem and continue reading further, click [here](http://home.netcom.com/~rogermw/Y2038.html).

Technorati Tags: Software Development, 2038, Y2k, Y3k, Computers, Programming, Time problem, Dates, IT industry, Bangalore, Bengaluru, Blog, Technology, Unix, Linux, Windows, Pc