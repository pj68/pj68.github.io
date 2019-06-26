

# setup raspGM as per the new videos



# initial install

- adjust the image size after install: 

sudo service docker stop

vim /usr/lib/systemd/system , change ExecStart=/usr/bin/dockerd to 
ExecStart=/usr/bin/dockerd --storage-opt dm.basesize=20G

sudo service docker start

docker info

- fetch the initial drjack image

sudo docker pull yavalek/drjack-wrf3


docker run -v /tmp/OUT:/root/rasp/PANOCHE/OUT -v /tmp/LOG:/root/rasp/PANOCHE/LOG --rm -it bash

video3:

xhost +

docker pull yavalek/drjack-wrf2-wrfsi

docker run -it -e DISPLAY=$DISPLAY -v /tmp/.X11-unix:/tmp/.X11-unix yavalek/drjack-wrf2-wrfsi

or

docker run -it -e DISPLAY=$DISPLAY --net=host --rm  yavalek/drjack-wrf2-wrfsi
./wrf_tools

video4:

docker build -t my-rasp-ec-4k .

docker run -v /tmp/OUT:/root/rasp/EC/OUT/ -v /tmp/LOG:/root/rasp/EC/LOG/  --rm my-rasp-ec-4k

docker build -t my-rasp-southcape-4k .

docker run -v /tmp/OUT:/root/rasp/SOUTHCAPE/OUT/ -v /tmp/LOG:/root/rasp/SOUTHCAPE/LOG/ --rm my-rasp-southcape-4k


## ftp setup

ssh-keygen

upload the ~/.ssh/id_rsa.pub to nearlyfreespeech.net, in the profile tab


system(" sftp -i /home/pj/.ssh/id_rsa -b /home/pj/wrf-portal/www/upload-blips.sftp paulhope_swiftsoft@ssh.phx.nearlyfreespeech.net  ")

## local docker setup's
natal:
``` 
cd /home/pj/docker/rasp-docker-script-master/drjack-wrf3-natal/
docker build -t my-rasp-natal-3k-12z-0day .

docker run -v /tmp/NATAL/OUT:/root/rasp/NATAL/OUT/ -v /tmp/NATAL/LOG:/root/rasp/NATAL/SOUTHCAPE/LOG/ --rm my-rasp-natal-3k-12z-0day:latest
```

## cloud deployment


 - build the image & tag with your dockerhub username

```
docker build -t my-rasp-eastcape-4k .

docker tag a4735d34ad5c paulhope/my-rasp-eastcape-3k-docker:20190403
```

 - save to a tar and split into chunks (note do not zip the file as the may be issues loading the doker image later) 

```
docker save -o ~/docker/my-rasp-eastcape-3k-docker.tar paulhope/my-rasp-eastcape-3k-docker:20190403

split -v 250M -d ec-4k.tar.gz
 ```
 - upload the chunks to a cloud instance (for goole cloud, start an instance, open the console, right click on the hub icon and select upload file)
 
 - on the cloud instance, join the images
 
 ```
 cat x* > my-rasp-eastcape-3k-docker.tar.gz
 ```
 
 - load the image
 ```
  docker load -i  my-rasp-eastcape-3k-docker.tar
 
 ```
 - push the image onto github
 
 ```
docker push paulhope/my-rasp-eastcape-3k-docker:20190403 
 ```
 
 misc....
 ```
docker run -v /tmp/EASTCAPE/OUT:/root/rasp/EASTCAPE/OUT/ -v /tmp/EASTCAPE/LOG:/root/rasp/EASTCAPE/LOG/  --rm -e INIT_TIME=0 -e START_HOUR=3 paulhope/my-rasp-eastcape-3k-docker:20190403


docker login --username=paulhope




docker push paulhope/my-rasp-eastcape-3k-docker:20190403




tar cvzf ec-4k.tar.gz my-rasp-eastcape-4k-pre.tar 

 split -v 250M -d ec-4k.tar.gz
cat x* > ec-4k.tar.gz
cat x* > my-rasp-eastcape-3k-docker.tar.gz

gunzip my-rasp-eastcape-3k-docker.tar.gz

```

### service-instance

```
curl http://metadata/computeMetadata/v1/instance/attributes/private-key -H "Metadata-Flavor: Google"
 sftp -i /home/paul_james_hope_68/.ssh/id_rsa paulhope_swiftsoft@ssh.phx.nearlyfreespeech.net


 python create_instance.py eastcape.cfg 0 auto-eastlondon-0
```

