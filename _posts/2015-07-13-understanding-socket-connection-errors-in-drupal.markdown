---
layout: post
title:  "Understanding socket connection errors in Drupal and how to solve them"
date:   2015-07-13 06:19:49
categories: PDOException, socket, errors, drupal 
banner_image: ""
featured: false
comments: true
---

In this post I will briefly record how to resolve the following error


    PDOException: SQLSTATE[HY000] [2002] Can't connect to local MySQL server through socket
    '/var/run/mysqld/mysqld.sock' (111) in lock_may_be_available() (line 167 of /var/www/drupal­
    7.22/includes/lock.inc).
    

This is a frustrating error which has made me go back to my web hosts and understand from them why this error repeated occurs. The biggest drawback of this error is that all drupal installations come to a halt for good and its a big journey from there until you screw up your databases, screw up your content and further are so misled by all explanations on the internet until you feel you are a dumbass for having to use drupal in the first place.

This is the cost of experimental software contributed by a community. Thankfully, [Jeffery Yee](https://plus.google.com/116304541579090621055/posts/AW7zehav7hS) has provided a solution for this and this is what you need to do to enjoy drupaling all over again.

**How to solve this issue?**
The solution that works best is to create a swap memory for mySQL and allow the applications to take advantage of that. Here’s how to do that:

* Login into your instance from Terminal or Command Prompt via SSH.
* Now, switch to Root mode (Sudo su)
* Run the following command: dd if=/dev/zero of=/swapfile bs=1M count=1024
* Make a swap file by running: mkswap /swapfile 
* Turn on Swap Files: swapon /swapfile

And that’s it. You’re done. To monitor your Swap file size and free space, just type swapon -s.