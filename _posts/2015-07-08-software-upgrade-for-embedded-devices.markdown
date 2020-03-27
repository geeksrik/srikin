---
layout: post
title:  "Software upgrade for embedded devices"
date:   2015-07-08 07:17:49
categories: OTA, usb, internet, upgrade, embedded, devices
banner_image: ""
featured: false
comments: true
---

From a long time, one of the major drawbacks of embedded systems was that software upgrade was almost impossible. But the scenario is quiet different in present day. Here, I have tried to give some insight into software upgradability in CE(Consumer electronics) products. In today’s digital world, we have transmission of programs in digital (DVB, ATSC etc), connectivity (HDMI, DVI etc) in digital, picture formats in digital( MPEG-2, MPEG-4 etc.). This is the driving factor for technological advancements in software upgradabilty feature.

There are various ways of upgrading software in embedded devices.Some of them are-

**1.OTA( Over The Air) download.** 

In this method, software image is transmitted along with normal TV programs. There are various open standards which support this. some of the well known are-

1.1 DVB SSU Signaling and Download- Receiver will be signalled about the image availabilty and it will have software to download the image.

1.2 DVB SSU Signaling Only – Receiver will capture signalling information and flash it to the user about the availabilty of new image. The software image itself will be delivered to the consumer by other means like FTP sites, CD shipment etc.

1.3Also, Satellite providers have custom solutions for delivering software image for their boxes. eg: TataSky,Foxtel etc have their own mechanisms for delivery of s/w over the air.

Some of the major factors to be considered in this method are – service provider selection, bandwidth selection, Duration of the software image to be aired etc…

Some of the devices which fall under this category are- Set Top Boxes, Digital Televisions, Digital Tuner based DVD recorders etc. The software which implements this feature is very complex. Sometimes, device manufactures decide to keep 2 copies of the image in the device as a recovery mechanism which increases the cost of device ( twice the size of flash required).

**2 Internet Based**

IP enabled devices can be easily upgraded by connecting to the corresponding server through internet.

Some of the devices which fall under this category are- IP Set Top Boxes, IP enabled Juke boxes, Divx Players etc.

**3 Other Mechanisms**

There are lots of other mechanisms, but not as popular as above two. some of them are-

3.1 USB based- download image into USB drive and connect the USB to the device to be upgraded. Eg: All Devices with USB port.

3.2 CD/DVD – Download image on to CD/DVD and upgrade.

Links: http://www.dvb.org/ , http://www.atsc.org/

Technorati Tags: Software Development, Software download, Over the air, OAD, DVB, SSU, IP based software upgrade. USB.