# nVidia 10 driver install

 - ref: https://docs.nvidia.com/cuda/cuda-installation-guide-linux/index.html
 
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
 
 ref: https://github.com/NVIDIA/nvidia-docker
 
 ```
  sudo yum install nvidia-docker2
 ```
 
 # nvidia .run driver install
 
 ref: http://www.advancedclustering.com/act_kb/installing-nvidia-drivers-rhel-centos-7/
 
 nvidia driver download:
 https://www.nvidia.com/object/unix.html
 
 - uninstall old vnidia driver
 ```
 /usr/bin/nvidia-uninstall
 ```
 - switch to text mode
```
sudo systemctl isolate multi-user.target 
 ```
 - install new cuda & driver
 ```
 /home/pj/cuda_10.0.130_410.48_linux
 ```
 - issue: segment fault on x startup, resolve by reinstalling x:
 ```
 yum reinstall xorg-x11-server-Xorg
 ```
 ref: http://rglinuxtech.com/?p=2423
 
 # nvidia cuda docker
 
 ref: https://hub.docker.com/r/nvidia/cuda/
 
 - build the container
 ```
 docker pull nvidia/cuda:10.0-cudnn7-devel
 docker build -t caffe2 .
 docker run  --runtime=nvidia -v  /tmp/deep:/root/share --rm -it  caffe2:latest bash
 ```
 - add the caffe src and build
```
find / -type f -name "*blas*.so"
```
 - add python caffe interface..
 ```
 apt install python-pip
 cd python
 for req in $(cat requirements.txt); do pip install $req; done
 
 make pycaffe
 export PYTHONPATH=/root/caffe/python:$PYTHONPATH
 export CAFFE_ROOT=/root/caffe

 ```
 - deepdream 
 
 ref: https://www.alanzucconi.com/2016/05/25/generating-deep-dreams/
 
 
  - build caffe
 ```
  cd ~\caffe

 make clean
 make all -j 8
 make test
 make runtest
 make distribute

```
- run deepdream
```
 cp distribute/lib/libcaffe.so distribute/python/caffe

 cp -r distribute/python/caffe /usr/local/lib/python2.7/dist-packages/caffe

 touch /etc/ld.so.conf.d/caffe.conf

 curl -O "http://dl.caffe.berkeleyvision.org/bvlc_googlenet.caffemodel"
 cd ~
 
 git clone https://github.com/google/deepdream.git

 
 
 sudo xhost +
 docker run --runtime=nvidia -it -e DISPLAY=$DISPLAY -v /tmp/.X11-unix:/tmp/.X11-unix -v /tmp/deep:/root/share --rm caffe2-3 bash

export PYTHONPATH=/root/caffe/python::/root/caffe/distribute/python/
 export LD_LIBRARY_PATH=:/root/caffe/distribute/python/caffe
 cd deepdream
 mkdir frames
 python dream.py

 ```

```
docker run  --runtime=nvidia -v  /tmp/deep:/root/share -e DISPLAY=$DISPLAY -v /tmp/.X11-unix:/tmp/.X11-unix  --rm -it  paulhope/caffe-deepdream:version1 bash

```

## network train

ref: https://www.facebook.com/groups/733099406836193/permalink/748784328601034


```
cd ~/caffe/models/MYNET
caffe train -solver ./solver.prototxt -weights ../bvlc_googlenet/bvlc_googlenet.caffemodel

caffe train -solver ./solver.prototxt -snapshot MYNET_iter_50000.solverstate

```

- mnist : http://caffe.berkeleyvision.org/gathered/examples/mnist.html

 ```
 cd ~/caffe
 ./examples/mnist/create_mnist.sh 
 ./examples/mnist/train_lenet.sh
 ```
 
 ## train new network
 
 ref: https://chunml.github.io/ChunML.github.io/project/Training-Your-Own-Data-On-Caffe/
 
 ```
 caffe train --solver=/root/caffe/models/mynet2_alexnet/solver.prototxt

 ```
