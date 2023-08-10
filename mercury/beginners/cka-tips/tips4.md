Drain nodes when maintenance needed
kubectl drain <nodename>
When its over you can use it again after the command bellow
kubectl uncordon <nodename>
when you want no more pods be scheduled on that node use 
kubectl cordon <nodename>

Upgrading kubernetes cluster
Verify the current version of the os
cat /etc/*release*
Verify version node 
kubectl get nodes

update version 
apt update
apt-cache madison kubeadm

select version

apt-mark unhold kubeadm && \
apt-get update && apt-get install -y kubeadm=<version> && \
apt-mark hold kubeadm

verify if upgrade download 
kubeadm version

verify upgrade plan 
kubeadm upgrade plan

apply upgrade 

sudo kubeadm upgrade apply <version>

then upgrade nodes 

sudo kubeadm upgrade node

drain the node

and upgrade cli 
apt-mark unhold kubelet kubectl && \
apt-get update && apt-get install -y kubelet=1.27.x-00 kubectl=1.27.x-00 && \
apt-mark hold kubelet kubectl
Restart the kubelet
sudo systemctl daemon-reload
sudo systemctl restart kubelet