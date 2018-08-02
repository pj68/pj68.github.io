---
layout: post
title:  Aqua
---

Summary: setup a standard centos 7 server

Hardware: intel i9 CPU 10 core, 16G DDR4 3000hz 4-channel, 500G SSD, nVidia Geforce 1070

Changelog:
 - install centos 7.1 from usb, developer packages, no seperate /home partition
 - update to latest packages: sudo yum update
 - install nvidia drivers
 - install vncserver: sudo yum install tigervnc
    ref: https://www.tecmint.com/install-and-configure-vnc-server-in-centos-7/
 - install gpuminer
 - install docker 
    ref: https://www.digitalocean.com/community/tutorials/how-to-install-and-use-docker-on-centos-7
    
