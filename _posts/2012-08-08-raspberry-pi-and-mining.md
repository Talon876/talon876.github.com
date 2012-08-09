---
layout: post
title: "Raspberry Pi and Mining"
tagline: "Mmmm.. Pi"
category: [statuses]
tags: [hardware, status]
---
{% include JB/setup %}
##Raspberry Pi
If you haven't heard about it already, the [Raspberry Pi](http://www.raspberrypi.org/faqs) is a $35 computer powered via micro USB and runs linux.
Or, a fancier description from the company:
>The Raspberry Pi is a credit-card sized computer that plugs into your TV and a keyboard. It's a capable little PC which can be used for many of the things that your desktop PC does, like spreadsheets, word-processing and games. It also plays high-definition video. We want to see it being used by kids all over the world to learn programming.

I ordered my Raspberry Pi a few months ago and I just got it a few days ago. It's been pretty fun to mess with so far.

*  One thing I've done with it is install [RaspBMC ](http://www.raspbmc.com/). 
It's a linux distro that boots directly in to the XBMC media player. Since the RPi can output over hdmi, this makes a great cheap home theater pc. I was able to play all of the SD content flawlessly off of my usb external hard drive.
It couldn't handle my 1080p content, but that wouldn't have been an issue if it was encoded using H.264.
*  I already have a htpc though so I've reflashed the SD card with Wheezy, a debian based linux distro.
I'm mostly just using it for tinkering at the moment and I hope to [connect it to a lapdock soon](http://rpidock.blogspot.com/2012/05/raspberry-pi-and-motorola-lapdock.html).
I've ordered all the parts, now I just have to wait.
*  I connected my RPi to a [PyMCU](http://pymcu.com/), a python controlled microcontroller.
{% assign image_id = "100" %}
{% assign alt_text = "Raspberry Pi connected to PyMCU" %}
{% include image %}

- - -

##BitCoin update
My last blog post was about [mining bitcoins](http://blog.nolat.org/statuses/bitcoins-and-hard-drives/) and I wanted to share some of the numbers so far!

Before I get to the numbers, I thought I'd share more information about the rig the graphics cards are mining in. (Keep in mind that I didn't buy these parts for mining, I 
just had them from an old computer)


####Desktop
*  __Motherboard:__ [Asus P6X58D](http://www.newegg.com/Product/Product.aspx?Item=N82E16813131614)
*  __Processor:__ [Intel Core i7-930 Bloomfield 2.8Ghz](http://www.newegg.com/Product/Product.aspx?Item=N82E16819115225)
*  __RAM:__ [Corsair Dominator 12GB (6 x 2gb)](http://www.newegg.com/Product/Product.aspx?Item=N82E16820145224)
*  __Graphics Cards:__ [Sapphire AMD Radeon HD 5830](http://www.ebay.com/itm/Sapphire-ATI-Radeon-HD-5830-1GB-256-bit-GDDR5-PCI-Express-2-1-x16-HDCP-100297L-/140801617126?pt=PCC_Video_TV_Cards&hash=item20c86e2ce6) x2
*  __Power Supply:__ [Corsair 850w](http://www.newegg.com/Product/Product.aspx?Item=N82E16817139009)
*  __Case:__ [Antec 1200 Full ATX](http://www.newegg.com/Product/Product.aspx?Item=N82E16811129043)
*  __Boot Drive:__ [1TB 7200rpm Sata 3.0Gb/s](http://www.newegg.com/Product/Product.aspx?Item=N82E16822152185)


I plan on moving my server programs off my main computer and on to this one since it could mine while doing simple server tasks. (More on 
that in a future post)

I roughly followed the [Complete Guide To Mine Bitcoin on Xubuntu 12.04](https://docs.google.com/document/d/1Gw7YPYgMgNNU42skibULbJJUx_suP_CpjSEdSi8_z9U/edit) guide while setting up my miner.

The main difference is I used Ubuntu 12.04 Desktop LTS.

Here is my mining script:

{% highlight bash %}
#!/bin/sh
export DISPLAY=:0
export GPU_USE_SYNC_OBJECTS=1
cd ~/cgminer-2.5.0-x86_64-built
./cgminer -o http://mine2.btcguild.com:8332 -u ******* -p **** --api-listen --api-network -I 9 --gpu-reorder --auto-fan --gpu-powertune 20 --gpu-engine 830-880  --gpu-memclock 300 -w 128 -g 3
{% endhighlight bash %}

I am also running openssh-server so I can ssh in to my miner and start/stop mining and check gpu temperatures.

###Mining Statistics

*  __Uptime:__ `~24/7`
*  __Average Mhash/sec:__ `580 Mhash/s`
*  __Pool:__ [BTCGuild](http://btcguild.com)
*  __Average Btc/day:__ `.26`
*  __Average Fan Speed:__ `GPU0: ~1700rpm` `GPU1: ~4200rpm`
*  __Average Temps:__ `GPU0: 73c` `GPU1: 83c`
