Setup Infiniband on CentOS 7

changelog:

ref:

https://www.slothparadise.com/setting-infiniband-centos-6-7/


yum -y groupinstall "Infiniband Support"

yum -y install infiniband-diags perftest gperf opensm

shutdown -r now

chkconfig rdma on

chkconfig opensm on


from history:
```
ifconfig
   98  ibstat
   99  ls /etc/infiniband
  100  ibstat
  101  ibnetdiscover
  102  ibnetdiscover --cache /tmp/inet_orig
  103  ibstat
  104  lspci |grep Mel
  105  ibv_devinfo
  106  ibhosts
  107  ibswitches
  108  lspci | grep -i infini
  109  sudo lspci -Qvvs 06:00.0
  110  udo mstflint -d 06:00.0 q
  111  sudo mstflint -d 06:00.0 q
  112  ibstat
  113  chkconfig opensm on
  114  chkconfig rdma on
  115  sudo \chkconfig rdma on
  116  opensm
  117  service rdma status
  118  service opensm status
  119  sudo service opensm status
  120  ibhosts
  ```
  
