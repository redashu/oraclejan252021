# k8s Revision 

<img src="rev.png">

## Installing k8s cluster in VMS/DC/Baremetal -- using kubeadm 

## prerequsite :
===

```
[root@ip-172-31-46-37 ~]# cat setup.sh 
# selinux security off
setenforce  0
sed -i 's/SELINUX=enforcing/SELINUX=disabled/'  /etc/selinux/config

## swap memory also off

swapoff -a

## enable kernel bridge network support 

modprobe br_netfilter
echo '1' > /proc/sys/net/bridge/bridge-nf-call-iptables

#  installing docker & kubeadm 

cat  <<EOF  >/etc/yum.repos.d/kube.repo
[kube]
baseurl=https://packages.cloud.google.com/yum/repos/kubernetes-el7-x86_64
gpgcheck=0
EOF

yum  install kubeadm  docker -y 

## starting docker & kubelet daemon 

systemctl start docker  kubelet 
systemctl enable  docker  kubelet 

```


## you can set hostname accordinly if required 

##  Now time to deploy master node component 

### use my github link :  https://github.com/reashu/k8s 

