---
layout: post
title:  "Codecs and container formats"
date:   2015-07-09 06:19:49
categories: Software Development, Technology Standards, MPEG, Codecs, Container formats, Standards, Compression, Divx, Video, Audio, Subtitles, Transport stream, Program stream, Elementary stream, Muxers, Demuxers, VLC, AVI, Ogg, MOV, ASF, MP4, MPEG-1, MPEG-2, MPEG-4, Vorbis, DivX, VOB, Video-LAN-Streaming, HowTo
handler
banner_image: ""
featured: false
comments: true
---

I found this snippet from the Video-LAN-Streaming HowTo document about Muxers and Codecs which clearly explains the possible video encoding formats, the container formats, the differences between container formats and codecs, etc. I am reproducing it here for reference and better understanding:

## What is a codec ? ##

To fully understand the VideoLAN solution, you must understand the difference between a codec and a container format A codec is a compression algorithm, used to reduce the size of a stream. There are audio codecs and video codecs.MPEG-1, MPEG-2, MPEG-4, Vorbis, DivX, … are codecs

## What is a container format ? ##

To start off, think of a container format as a standard shipping box. You get a box in the mail and you think, "Cool! What’s inside." You don’t really care about the box itself, you care about what’s in that box. The problem? You can’t see into the box. So what do you do? You get a knife and cut it open.
A container format follows this same basic idea. It contains one or several streams already encoded by codecs. Very often, there is an audio stream and a video one. AVI, Ogg, MOV, ASF, MP4 … are container formats. The streams contained can be encoded using different codecs. In a perfect world, you could put any codec in any container format. Unfortunately, there are some incompatibilities. You can find a matrix of possible codecs and container formats on the features page (http://www.videolan.org/streaming/features.html)

## Encoding a video ##

This is the first step where you are going to create the shipping box. First you need to encode your file. That means that a file, wheter it is an audio, video file, is compressed to another format that normally takes up less physical drive space than the previous format. Common video encoding methods are DivX, MPEG-1, MPEG-2, MPEG-4 … most common audio encoding method is MP3 or ogg-vorbis. Then you have to mux (or multiplex). This means basically a process where separate parts of the video (or streams) are joined together into one file.

## Playing a video ##

Now that you have your box, you need to open it before to see the content. That’s exactly what VLC will do. To decode a stream, VLC first demuxes it. This means that it reads the container format and separates audio, video, and subtitles, if any. Demuxing files doesn’t weaken the video nor audio quality, it doesn’t do anything for these data streams, it justs simply saves them into separate files, each containing one element of the original file. Then, each of these are passed decoders that do the mathematical processing to decompress the streams.

## There is a particular thing about MPEG ##

- MPEG is a codec. There are several versions of it, called MPEG-1, MPEG-2, MPEG-4, …
- MPEG is also a container format, sometimes refered to as MPEG System. 

There are several types of MPEG: ES, PS, and TS.
When you play an MPEG video from a DVD, for instance, the MPEG stream is actually composed of several streams (called Elementary Streams, ES): there is one stream for video, one for audio, another for subtitles, and so on. These different streams are mixed together into a single Program Stream (PS). So, the .VOB files you can find in a DVD are actually MPEG-PS files. But this PS format is not adapted for streaming video through a network or by satellite, for instance. So, another format called Transport Stream (TS) was designed for streaming MPEG videos through such channels.

Technorati Tags: Software Development, Technology Standards, MPEG, Codecs, Container formats, Standards, Compression, Divx, Video, Audio, Subtitles, Transport stream, Program stream, Elementary stream, Muxers, Demuxers, VLC, AVI, Ogg, MOV, ASF, MP4, MPEG-1, MPEG-2, MPEG-4, Vorbis, DivX, VOB, Video-LAN-Streaming, HowTo