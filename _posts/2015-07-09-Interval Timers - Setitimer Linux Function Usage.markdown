---
layout: post
title:  "Interval Timers :: Setitimer Linux Function Usage"
date:   2015-07-09 06:09:49
categories: Software Development, Timers, Setitimer, Interval timer, Linux, C, Timer handler
banner_image: ""
featured: false
comments: true
---

The setitimer call in linux is used to set the timer provided to a process by the kernel to a specific value. When it expires, a designated callback can be called. I had a situation where I needed one such timer which would alert my module once expired. But some things about setitimer are best noted here:

The set interval timer function in linux has the following signature:

SYNOPSIS

<pre>
#include <sys/time.h>

int setitimer (int which, const struct itimerval *value, struct itimerval *ovalue);

</pre>

It is used to create a timer which will alert the process by calling a callback once the timer expires.
If you look at the following piece of code

<pre>
int SetTimerAndStart(funcPtr pFunc, long int TimerValue)
{
int result = 0;
long int timervalue = 1;

struct itimerval value, ovalue, pvalue;
int which = ITIMER_REAL;

struct sigaction sact;
volatile double count;
time_t t;

sigemptyset( &sact.sa_mask );
sact.sa_flags = 0;
sact.sa_handler = pFunc;
sigaction( SIGALRM, &sact, NULL );

getitimer( which, &pvalue );

//Set a real time interval timer here
value.it_interval.tv_sec = TimerValue; /* seconds */
value.it_interval.tv_usec = 0; /* milliseconds */
value.it_value.tv_sec = TimerValue; /* reset to seconds */
value.it_value.tv_usec = 0; /* reset to milliseconds */

result = setitimer( which, &value, &ovalue );
return result;
}
</pre>

this function takes in a function pointer of the form void (*ptr)(int sig) and a long integer value which is set to the tv_sec variable within the function.

Now I made a call to this function with the following

int ret = SetTimerAndStart(HandlerFunc, 5)

Handler func was of type void HandlerFunc(int) and I wanted the timer for 5 seconds. On a bare look at this code everything seems fine since it means I am asking for a timer with timeout of 5 seconds. But did this work for me?

The answer is no. The code core dumped when it was run leaving me confounded for a while. It is then that I realized the rather very silly error in the call which was causing a problem. It was the value 5 being passed as a long int.

The correct call to be made was as shown below:

long int value = 5;
int ret = SetTimerAndStart(HandlerFunc, value);

Now I ll leave you to analyse why the former did not work, and why the latter call worked. But remember: BOTH CALLS DID COMPILE! 
More posts will be following on this topic later!

Technorati Tags: Software Development, Timers, Setitimer, Interval timer, Linux, C, Timer handler