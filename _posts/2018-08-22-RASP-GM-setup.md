

# setup raspGM as per the new videos



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


# ftp setup

ssh-keygen

upload the ~/.ssh/id_rsa.pub to nearlyfreespeech.net, in the profile tab


system(" sftp -i /home/pj/.ssh/id_rsa -b /home/pj/wrf-portal/www/upload-blips.sftp paulhope_swiftsoft@ssh.phx.nearlyfreespeech.net  ")

