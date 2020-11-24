---
title: "iMac 2009: Supported Linux Distribution in November 2020"
description: "A list of Linux distributions I could make working on my iMac early 2009"
authors: ["Xavier Camier"]
date: 2020-11-24T16:07:32+01:00
tags: ["System","Linux"]
images: ["linux.png"]
draft: false
---

### Introduction

The only goal of that article is to provide a list of linux distribution that I have tested on my early 2009 iMac and to differentiate those I could make working from the others. 

What has been tested:
- Ability to run the livecd mode through USB (iso -> etcher -> USB Key)
- Ability to display the desktop
- Working ethernet connection
- Ability to browse through the default browser
- Ability to manipulate few files through the file manager


### Results

#### Linux distributions I could make working

| Distribution Name | ISO Name                          | Observation                                  |
| ----------------- |-----------------------------------| ---------------------------------------------|
| Ubuntu 19.10      | ubuntu-19.10-desktop-amd64.iso    | /                                            |
| Ubuntu 20.04      | ubuntu-20.04.1-desktop-amd64.iso  | Few errors at startup. No consequence        |
| Ubuntu 20.10      | ubuntu-20.10-desktop-amd64.iso    | Few errors at startup. No consequence        |
| Mint 20           | linuxmint-20-cinnamon-64bit.iso   | Few errors at startup. No consequence        |


#### Linux distributions I could not make working

| Distribution Name | ISO Name                                | Observation                                  |
| ----------------- |-----------------------------------------| ---------------------------------------------|
| Elementary OS 5.1 | elementaryos-5.1-stable.20200814.iso    | Could start but freeze when using it. Minimal reqs suggest core i3 as minimal proc, iMac has a Core 2 Duo. That may explain why                                 |
| Manjaro 20.1.2    | manjaro-gnome-20.1.2-201019-linux58.iso | Doesn't even start.                          |
