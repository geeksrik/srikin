---
layout: post
title:  "Usage of timers - what you need to know about them?"
date:   2015-07-09 06:08:49
categories: Software Development, Timeval, ITimer, SetITimer, GetITimer, Linux, Unix, Timers, Signals, Signal handler, Usage, Sigalrm, Real timer, Virtual timer, Prof timer, Man, Bangalore, Bengaluru, Technology, Blog
banner_image: ""
featured: false
comments: true 
---

I had written an earlier article on Timers in Linux. In this article I share with you a slideshow on what is possible with timers and what is not achievable, so that you may clearly understand how timers can be used during system programming under a linux host or linux target based environment.

<iframe src="http://www.slideshare.net/slideshow/embed_code/274711" width="597" height="486" frameborder="0" marginwidth="0" marginheight="0" scrolling="no" style="border:1px solid #CCC;border-width:1px 1px 0;margin-bottom:5px" allowfullscreen> </iframe>


----------


The following points are worth noting about timers

* The time is stored relative to a certain date in history (Jan 1, 1970), so when you read the time, its always a number relative to this date. This is called EPOCH time or the UNIX EPOCH time.
* Each process is allocated one timer, this is called per process timer.
* iTimers which are of three types: REAL, VIRTUAL and PROF
* how to initialize countdown timers and use them
* iTimerVal and timeval structures
* it_interval, it_value, tv_sec, tv_usec variables and their possible values
* using the signal handler function to handle timer expiry signals
* how to set signal handlers while using timers
* types of signals that can be sent to process or across processes (SIGALRM)


So its now easy for you to write a small timer program in linux and compile it using the following :

<pre>
gcc timer_example.c p-o timer_example
</pre>

run it using

<pre>
./timer_example
</pre>

and check your logs to see if the timers did expire properly! As you would be aware the timer is a per process timer which means within a process, if you require timeouts at different intervals it has to be an enhancement over a single timer. So you could expire a single timer every say 1 second or 10 milliseconds or whatever value you want (at a granular level) and provide a specific interrupt to the process or other processes every "N" seconds or milliseconds where "N" is a multiple of the it_value variable within the timeval structure.

Try it out yourself and be rest assured it ll work like a charm.

Technorati Tags: Software Development, Timeval, ITimer, SetITimer, GetITimer, Linux, Unix, Timers, Signals, Signal handler, Usage, Sigalrm, Real timer, Virtual timer, Prof timer, Man, Bangalore, Bengaluru, Technology, Blog