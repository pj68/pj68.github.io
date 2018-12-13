---
layout: post
title: DeepDream
---

##DeepDream

- install docker

- install nvidia-docker2

- create docker: dream1
Dockerfile:
```
FROM nvidia/cuda:9.0-cudnn7-devel
RUN mkdir /root/deep
RUN mkdir /root/deep/share
WORKDIR /root/deep/
VOLUME ["/root/deep/share"]
```
build commands:
```
sudo docker build -t dream1 .
sudo docker run  --runtime=nvidia -v  /tmp/deep:/root/deep/share --rm -it  dream1:latest bash
```
docker build commands
```
apt-get install libprotobuf-dev libleveldb-dev libsnappy-dev libopencv-dev libhdf5-serial-dev protobuf-compiler

apt-get install --no-install-recommends libboost-all-dev

chmod a+x share/Anaconda3-5.3.1-Linux-x86_64.sh

share/Anaconda3-5.3.1-Linux-x86_64.sh

apt-get install libatlas-base-dev 
```

- install caffe


caffe ref:

http://caffe.berkeleyvision.org/installation.html

ref:

http://korbonits.github.io/2015/07/29/Caffe-brew-your-first-DNN.html
