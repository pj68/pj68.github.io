---
layout: post
title:  Folding
---


# Folding@home

### Centos Setup

#### install
- download the tar's from https://foldingathome.org/
- extract
```
sudo rpm -ivh fahclient-7.5.1-1.x86_64.rpm
sudo rpm -ivh fahcontrol-7.5.1-1.noarch.rpm
```
- run FAHControl from the icon on the desktop

#### Tips
 - if there is trouble with the FAHControl GUI not recognising the Nvidia drivers on can run the FAHClient from the command line
```
 su
 cd /usr/bin
 ./FAHClient
```

note: the config.xml will be created in the current directory, one can edit it to add, eg usrename tag, etc, for more comman line control one can use the FAHControlWrapper
 an example config.xml:
```
<config>

 <user v='paulhope68' />

  <!-- Folding Slots -->
  <slot id='0' type='CPU'/>
  <slot id='1' type='GPU'/>
</config>

```

#### review stats
use the username in the url, eg https://stats.foldingathome.org/donor/paulhope68
