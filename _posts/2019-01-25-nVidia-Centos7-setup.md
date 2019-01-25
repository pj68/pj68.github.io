# nVidia 10 driver install

 - ref: 
 
 install:
 ```
 uname -m && cat /etc/*release
 uname -r
 gcc --version

 sudo yum install kernel-devel-$(uname -r) kernel-headers-$(uname -r)
 
  sudo yum localinstall --nogpgcheck https://download1.rpmfusion.org/free/el/rpmfusion-free-release-7.noarch.rpm https://download1.rpmfusion.org/nonfree/el/rpmfusion-nonfree-release-7.noarch.rp
  
 
 ```
 
 ## issues
- conflicts,  attempts:
 ``` 
 yum clean expire-cache
 yum-config-manager  --disable nux-dextop 
 yum install cuda
  yum erase xorg-x11-drv-nvidia
 
 ```
 
 # nvidia docker 2 install
 
 
 ```
  sudo yum install nvidia-docker2
 ```
