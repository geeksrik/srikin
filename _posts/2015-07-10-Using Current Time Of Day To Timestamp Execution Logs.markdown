---
layout: post
title:  "Using Current Time Of Day To Timestamp Execution Logs"
date:   2015-07-10 06:08:49
categories: Software Development, Timers, Timeofday, Time_t, Timeval, Strftime, Unix, Linux, Programming, Bangalore, Bengaluru, Technology, Blog, Software development, Tv_usec, Tv_sec
banner_image: ""
featured: false
comments: true
---

I keep coming back to timers these days as my work is involving their usage heavily  -). The latest was a requirement by me for knowing a current time for timestamping a certain sequence of logs. I found this program at a sourceforge website, which just wonderfully and blissfully did what I wanted …

Here is the small tiny program for reference:


    /* C routine: sample gettimeofday with time in milliseconds
       mmc mchirico@users.sourceforge.net
    
       Downloads:
    
    http://prdownloads.sourceforge.net/cpearls/date_calc.tar.gz?download
    
    */
    #include <sys/time.h>
    #include <time.h>
    #include <stdlib.h>
    #include <stdio.h>
    
    int mainvoid
    {
      char buffer[30]
      struct timeval tv
    
      time_t curtime
    
      gettimeofday&tv, NULL
      curtime=tv.tv_sec
    
      strftimebuffer,30,"%m-%d-%Y  %T.",localtime&curtime
      printf"%s%ld’n",buffer,tv.tv_usec
    
      return 0
    
    }



My execution logs looked something like this:

    
    RESULT : EName:[02-25-2008 15:26:50.MS: 520548] Sub : –[1]– EvID : –[1]– Pub : –[0x9163788]– PName : –[pub1]–
    RESULT : EName:[02-25-2008 15:26:50.MS: 520708] Sub : –[1]– EvID : –[1]– Pub : –[0x91638d0]– PName : –[pub2]–
    RESULT : EName:[02-25-2008 15:26:50.MS: 520799] Sub : –[1]– EvID : –[1]– Pub : –[0x91639f8]– PName : –[pub3]–
    


Technorati Tags: Software Development, Timers, Timeofday, Time_t, Timeval, Strftime, Unix, Linux, Programming, Bangalore, Bengaluru, Technology, Blog, Software development, Tv_usec, Tv_sec
