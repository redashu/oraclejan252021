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



## Pod deployment 

```
❯ kubectl  get  po
NAME           READY   STATUS    RESTARTS   AGE
ashu-pod-1     1/1     Running   0          93s
manju-pod-1    1/1     Running   0          36s
sam-pod-2      1/1     Running   0          31s
venkat-pod-1   1/1     Running   0          16s
❯ 
❯ kubectl  get  nodes
NAME            STATUS   ROLES                  AGE   VERSION
master-node     Ready    control-plane,master   29m   v1.20.2
minion-node-1   Ready    <none>                 28m   v1.20.2
minion-node-2   Ready    <none>                 28m   v1.20.2
minion-node-3   Ready    <none>                 28m   v1.20.2
❯ kubectl  get  po   -o wide
NAME           READY   STATUS    RESTARTS   AGE     IP               NODE            NOMINATED NODE   READINESS GATES
ashu-pod-1     1/1     Running   0          3m21s   192.168.97.65    minion-node-2   <none>           <none>
manju-pod-1    1/1     Running   0          2m24s   192.168.97.66    minion-node-2   <none>           <none>
sam-pod-2      1/1     Running   0          2m19s   192.168.138.66   minion-node-1   <none>           <none>
venkat-pod-1   1/1     Running   0          2m4s    192.168.97.67    minion-node-2   <none>           <none>

```

## accessing application running in the pod using kubectl port-forward

<img src="portf.png">

## intro to service in k8s

<img src="service.png">

## service find pod using label 

<img src="s2label.png">

## type fo service in k8s

<img src="stype.png">

## nodeport service 

<img src="np.png">

## explain nodeport 

<img src="expnp.png">

## Deploy / update label of pod 

```
apiVersion: v1 # this is api version for pod 
kind: Pod # requesting api server about Pod 
metadata:
 name: ashu-pod-1 # name of POD
 labels: # to define label 
  x: helloashu #  label must be in a key: value format 
spec:
 containers: # here will write about container from any CRE
 - image: nginx # image from docker hub 
   name: ashuc1 # name of container 
   ports:  # port of application in side container 
   - containerPort: 80  
   
 ```
 
 ## checking labels 
 
 ```
 ❯ kubectl get po  --show-labels
NAME           READY   STATUS    RESTARTS   AGE   LABELS
ashu-pod-1     1/1     Running   0          47m   x=helloashu
manju-pod-1    1/1     Running   0          66m   <none>
niran-pod-1    1/1     Running   0          61m   <none>
sam-pod-2      1/1     Running   0          66m   run=sam-pod-2
sat-2          1/1     Running   0          62m   x=satlab1
suresh-pod-1   1/1     Running   0          60m   <none>

```

## creating nodeport service 

```
❯ kubectl create  service  nodeport ashus1 --tcp 1234:80   --dry-run=client -o yaml
apiVersion: v1
kind: Service
metadata:
  creationTimestamp: null
  labels:
    app: ashus1
  name: ashus1
spec:
  ports:
  - name: 1234-80
    port: 1234
    protocol: TCP
    targetPort: 80
  selector:
    app: ashus1
  type: NodePort
status:
  loadBalancer: {}
❯ kubectl create  service  nodeport ashus1 --tcp 1234:80   --dry-run=client -o yaml   >ashusvc1.yaml

```

