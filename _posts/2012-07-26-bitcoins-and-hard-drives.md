---
layout: post
title: "Bitcoins and Hard drives"
tagline: "[money and space]"
category: [statuses]
tags: [hardware, status]
---
{% include JB/setup %}
I took a short break from writing for awhile. So here's an update!

I've been a fan of [bitcoins](http://bitcoin.org/about.html) for awhile now. I won't explain them in depth in this post as there are much better resources elsewhere on the Internet.

I started mining bitcoins almost a year ago with my `AMD HD 6950` graphics card which has worked wonderfully. Sadly, I've sold bitcoins at times when I should have waited, but even with my lack of "stock" knowledge, I've earned a decent amount of dollars with them.

Recently, their prices have been rising and are becoming more stable, and I've [upgraded my computer](http://blog.nolat.org/statuses/battlestation-hardware/) since then.

This left my old computer just sitting around being a (pretty bad) file server. Not anymore!

###Dedicated Bitcoin Miner

I will now be using my old computer as a dedicated bitcoin miner, and possibly Jenkins/Sonar/Tomcat/Apache/MySQL server. For the time being, just a bitcoin miner is all I need as my current desktop functions as all the other servers.

*  I bought two `AMD HD 5830`'s to mine with.
{% assign image_id = "70" %}
{% assign alt_text = "Bitcoin mining rig + graphics cards" %}
{% include image %}

*  There's still a decent amount of room in the case (since I removed 4 hard drives).
{% assign image_id = "80" %}
{% assign alt_text = "Bitcoin mining rig with graphics cards" %}
{% include image %}


It'll probably take a few months before I break even from buying the cards, but after that it's pure profit.

###Hard Drives
That old computer had 5 hard drives in it. They also had a lot of duplicate and triplicate copies of data so I'm going through and copying important files to my new computer and then I will be formatting them all.

I ended up removing four hard drives (1 1tb drive remained in the mining computer):

*  1x 1tb 7200rpm - Going in my other server
*  1x 500gb 7200rpm - Selling to a friend
*  1x 400gb 7200rpm - Possibly selling to a friend
*  1x 160gb SSD - Going in my laptop

I took this opportunity to test the sata to USB3.0 connectors that I had leftover from [disassembling 3tb external hard drives](http://blog.nolat.org/tutorials/3tb-hdd-for-129-99/).

*  They work great!
{% assign image_id = "90" %}
{% assign alt_text = "Sata to usb3.0 connector" %}
{% include image %}

All you have to do is put a hard drive on it, the sata/power ports line up just fine (as you would expect). Windows recognized the drive immedietly and everything was there (though it was formatted as NTFS, other formats may not be as cooperative). The only downside is the file transfer rate isn't as good but there could be other factors involved. Such as the fact that this hard drive is from my computer from 2008 and hasn't been defragmented in years.