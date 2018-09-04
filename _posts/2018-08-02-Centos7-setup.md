---
layout: post
title:  CentOS 7 Setup
---

Summary: setup a standard centos 7 server

Hardware: intel i9 CPU 10 core, 16G DDR4 3000hz 4-channel, 500G SSD, 2x office trnVidia Geforce 1070

Changelog:

 - install centos 7.1 from usb, developer packages, no seperate /home partition
 
 - update to latest packages: sudo yum update
 
 - install nvidia drivers
 
 - install vncserver: 
 
    ref: https://www.tecmint.com/install-and-configure-vnc-server-in-centos-7/ 
    
    edit ~/.vnc/xstartup replace last line with startkde &
    
    vncserver :3 -geometry 2000x1400 -extension RANDR 
    
 - install gpuminer
 
 - install vsftp 
 
    ref: https://www.liquidweb.com/kb/how-to-install-and-configure-vsftpd-on-centos-7/ 
    
    https://linuxconfig.org/rhel7-ftp-server-error-ftp-connect-no-route-to-host-solution
    
 - install docker 
 
    ref: https://www.digitalocean.com/community/tutorials/how-to-install-and-use-docker-on-centos-7
    
