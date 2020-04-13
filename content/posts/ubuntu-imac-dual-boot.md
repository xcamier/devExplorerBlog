---
title: "Installation of Ubuntu in dual boot with El Capitan"
description: "How to install Ubuntu in dual boot with El Capitan on an early 2009 iMac"
authors: ["Xavier Camier"]
date: 2020-04-08T12:00:00+02:00
tags: ["System","Linux","OSX","Tutorial"]
images: ["ubuntu.jpg"]
draft: false
---

I bought my 24' iMac in March 2009. The latest OSX Version it can support is El Capitan. Althought it is still a very capable machine with its 8 Gb of RAM and its new SSD, the lack of OSX update makes its support of new iCloud features more and more limited. And I can't convert it to a dev machine as the last version of .net core it supports is 2.2. I need 3.1 to play with Blazor. In fact all I use that machine for is to talk with my associates with Teams, to surf the internet a bit, to listen to the music and for the iMessage client. It's time to give that machine a second life thanks to linux !

This article describes wow I have installed ubuntu 19.10 in dual boot with El Capitan. It's pretty easy.

1. Boot on the mac in recovery mode and start the command line (hold cmd+r at startup)
2. From the menu open the terminal and run

{{< highlight bash "linenos=table,hl_lines=6 15-17,linenostart=1" >}}
csrutil disable; reboot
{{< / highlight >}}

3. Boot to mac os
4. Download rEFInd boot manager on the and install it using the provided script
5. Open the OSX disk tool
6. Create a partition for linux installation: name it linux to find it easily later. Format it in FAT
7. Create a partition for the linux swap (optional): name it swap and format it in FAT. Suggested size: (ram + sqrt ram) 
8. Plug your USB key with the Ubuntu version
9. Restart the computer in holding "alt" and choose the USB key as booting device
10. Install ubuntu => use the two FAT partitions for the install (/) and for the swap. It should format them in ext4
11. Let the installer doing its job. It may take time.

---

Sources :

https://rodsbooks.com/refind

https://www.howtogeek.com/187410/how-to-install-and-dual-boot-linux-on-a-mac/

https://linuxnewbieguide.org/how-to-install-linux-on-a-macintosh-computer/