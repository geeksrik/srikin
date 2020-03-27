---
layout: post
title:  "Enabling TFTP Based Linux Kernel Boot Up"
date:   2015-07-08 04:07:49
categories: TFTP, linux, kernel, bootup
banner_image: ""
featured: false
comments: true
---

**TFTP** (or Trivial File Transfer Protocol) is used by the boot rom in several vendors’ machines to download the boot loader and/or the kernel. This service runs over TCP/IP, so the client must first obtain an IP address, typically via rarp, bootp, or dhcp means

1. firstly there should be a directory called ‘tftpboot’ under ‘/’, if not this must be set up by doing a mkdir -p /tftpboot (this is on the linux host and not on target) 
2. copy the linux kernel into this directory 
3. we also need to start the tftp service if not already there, with some minor changes 
4. edit the file /etc/xinetd.d/tftp and change the value ‘disable’ to ‘no’ from ‘yes’



<pre>
# default: off 
# description: The tftp server serves files using the trivial file transfer \ 
# protocol. The tftp protocol is often used to boot diskless \ 
# workstations, download configuration files to network-aware printers, \ 
# and to start the installation process for some operating systems. 
service tftp 
{ 
socket_type = dgram 
protocol = udp 
wait = yes 
user = root 
server = /usr/sbin/in.tftpd 
server_args = -s /tftpboot 
disable = no <<<<<<<<<<<<<<<<<<<<<<<<<<<<<<< 
per_source = 11 
cps = 100 2 
flags = IPv4 
}</pre>


* Save the file, and restart the xinetd service by issuing ‘/sbin/service xinetd restart’ 
* now the TFTP service should be started and the linux kernel should be available for boot from the target side.

and finally on a target which has a CFE terminal (Custom Firmware Extender), we can use a command such as :

`boot -z -elf vvv.xxx.yyy.zzz:vmlinuz_full_kernel_name ‘console=<console_name>,<baud_rate> rootfstype=<root file system type> root=<partition name for root dir> <mode of boot for this file sys> ‘`

vvv.xxx.yyy.zzz = the IP address of the linux host which has the linux kernel to be used for booting target

some typical examples for

`console name = ttys1, ttys2, etc 
baud rate = 115200, 9600 etc 
rootfstype = ext3, swap etc 
partition name = /dev/hda1, /dev/sda3, etc 
mode of boot = r – read, w – write, rw – read/write`

**NOTE**: it is important that we first set up the target board for ethernet connectivity via DHCP or other means such as giving it a static IP address 
This is easily done with the command: ifconfig eth0 -addr=155.44.55.77;

