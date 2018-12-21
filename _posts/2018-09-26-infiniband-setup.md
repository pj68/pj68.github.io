Setup Infiniband on CentOS 7

changelog:

ref:

https://www.slothparadise.com/setting-infiniband-centos-6-7/


yum -y groupinstall "Infiniband Support"

yum -y install infiniband-diags perftest gperf opensm

shutdown -r now

chkconfig rdma on

chkconfig opensm on
