---
layout: post
title:  "Tm To Epoch Time Conversion"
date:   2015-07-09 06:09:49
categories: Software Development, Epoch, Unix epoch, Software Development, Timeval, ITimer, SetITimer, GetITimer, Linux, Unix, Timers, Signals, Signal handler, Usage, Sigalrm, Real timer, Virtual timer, Prof timer, Man, Bangalore, Bengaluru, Technology, Blog, Mktime, Tm to epoch, Tm, Time_t, Linux, Programming, Timers, Opengroup
banner_image: ""
featured: false
comments: true 
---



Linux provides a friendly way of entering time in terms of details such as day month year, seconds, hours, minutes etc. The structure in question is called "tm" and is as shown below:

<pre>
struct tm
{
int tm_sec;
int tm_min;
int tm_hour;
int tm_mday;
int tm_mon;
int tm_year;
int tm_wday;
int tm_yday;
int tm_isdst;
}
</pre>

However for comparisons, this time has to be further converted to the standard UNIX EPOCH time discussed in earlier articles. So for this, a function called mktime does this necessary conversion and provides a result in the form time_t which is in effect an epoch time. Two epoch times can be compared with relational operators (<, >, = =, !=) and we can decide which of the two input times is greater than the other or lesser than that other, etc.

An example from the opengroup is provided here for reference

What day of the week is July 4, 2001?


    #include <stdio.h>
    #include <time.h>
    
    struct tm time_str;
    
    char daybuf[20];
    
    int main(void)
    {
        time_str.tm_year = 2001 - 1900;
    	time_str.tm_mon = 7 - 1;
    	time_str.tm_mday = 4;
    	time_str.tm_hour = 0;
    	time_str.tm_min = 0;
    	time_str.tm_sec = 1;
    	time_str.tm_isdst = -1;
    	if (mktime(&time_str) == -1)
    		(void)puts("-unknown-");
    	else {
    		(void)strftime(daybuf, sizeof(daybuf), "%A", &time_str);
    		(void)puts(daybuf);
    	}
    	return 0;
    }
    

Its worthy to note here that the call can return a value if -1 (casted to time_t) if in case the resultant output cannot be expressed in the form of an epoch time.

You can try out the function mktime with a few input examples for the struct tm, on your own, to see the results for yourself. Try some invalid values as well.

Technorati Tags: Software Development, Epoch, Unix epoch, Software Development, Timeval, ITimer, SetITimer, GetITimer, Linux, Unix, Timers, Signals, Signal handler, Usage, Sigalrm, Real timer, Virtual timer, Prof timer, Man, Bangalore, Bengaluru, Technology, Blog, Mktime, Tm to epoch, Tm, Time_t, Linux, Programming, Timers, Opengroup
